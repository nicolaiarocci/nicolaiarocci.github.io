---
date: 2021-11-14T07:05:25+01:00
title: "My ASP.NET 5 migration to .NET 6"
share: false
tags: ["aspnet", "dotnet", "programming"]
---
I spent the last few days migrating our ASP.NET REST services, MVC web
applications and Blazor server apps to .NET 6. Overall the process was pretty
straightforward. The few issues I went through were easy to solve and well
documented. Things got more involved with the EF Core 6 transition, especially
with the Npgsql Entity Framework Core Provider.

The official [ASP.NET Core 5.0 to 6.0 migration guide][1] was my first stop. It
offers the perfect entry point, rich with in-depth links. At this stage, I am
not interested in switching to the new .NET 6 minimal hosting model (aka
Minimal APIs). I think it's a significant improvement, and we will likely adopt
it for new projects, but our production projects aren't going to be refactored
right away. Should minimal APIs also prove to be remarkably performant, we'll
reconsider them[^11].

The first step was updating the target framework moniker to `net6.0`.

    <Project Sdk="Microsoft.NET.Sdk.Web">
      <PropertyGroup>
        <TargetFramework>net6.0</TargetFramework>
      </PropertyGroup>
    </Project>


Then, I updated all `Microsoft.AspNetCore.*` and `Microsoft.Extensions.*` package
references to version 6.0.0. 

    <ItemGroup>
      <PackageReference Include="Microsoft.AspNetCore.JsonPatch" Version="6.0.0" />
      <PackageReference Include="Microsoft.Extensions.Caching.[...]" Version="6.0.0" />
    </ItemGroup>

That's all I needed to do to update the MVC application. The only other thing
left for me was to update Dockerfile's `FROM` statements to pull the new .NET
6 image:

    # build stage
    FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
    WORKDIR /build
    [..]
    # final stage/image
    FROM mcr.microsoft.com/dotnet/aspnet:6.0
    [..]

Migrating the WebApi/REST services required more work. I got a few errors and
warnings, either at compile or runtime. Let's go through them one by one.

### New `JsonSerializer` source generator overloads

> The call is ambiguous between the following methods or properties:
> 'JsonSerializer.Serialize(TValue, JsonSerializerOptions?)' and
> 'JsonSerializer.Serialize(TValue, JsonTypeInfo)'"

In .NET 6, the `Sytem.Text.Json.JsonSerializer` [acquired two new overloads][2] that
support pre-generated type information via source-generators. Previously, you
could write code that passed `null` (or `default`) as the value for the
`JsonSeralizerOptions` parameter:

    entity.Property(e => e.Value)
        .HasConversion(
            v => JsonSerializer.Serialize(v, null),
            v => JsonSerializer.Deserialize(v, null));

However, the new source-generator-enabled overloads will cause ambiguity if you
pass `null`. The solution was to add simply an explicit cast to the intended
target:

    entity.Property(e => e.Value)
        .HasConversion(
            v => JsonSerializer.Serialize(v, (JsonSerializerOptions)null), 
            v => JsonSerializer.Deserialize(v, (JsonSerializerOptions)null));

### The `RNGCryptoServiceProvider` is now obsolete

> SYSLIB0023: RNGCryptoServiceProvider is obsolete

As it turns out, `RNGCryptoServiceProvider` is [marked as obsolete in .NET 6][3]. The
new preferred way to generate a random number is using one of the
`RandomNunmberGenerator` static methods.

      // old
      using var rng = new RNGCryptoServiceProvider();
      var uintBuffer = new byte[sizeof(uint)];
      rng.GetBytes(uintBuffer);
      var num = BitConverter.ToUInt32(uintBuffer, 0);

      // new
      using var rng = RandomNumberGenerator.Create();
      var uintBuffer = new byte[sizeof(uint)];
      rng.GetBytes(uintBuffer);
      var num = BitConverter.ToUInt32(uintBuffer, 0);

The two issues above are essentially the only ones I met with .NET 6 itself. As
mentioned, I also encountered a few EF Core 6 annoyances. They are listed
below.

### New `IModelCacheKeyFactory.Create()` overload

> The requested configuration is not stored in the read-optimized model, please
> use DbContext.GetService&lt;IDesignTimeModel&gt;().Model.

If, like me, you happen to have a custom `IModelCacheKeyFactory`
implementation, you will likely get this error at runtime. Starting with EF
Core 6, [you must implement][4] the new overload of the `Create` method that
handles design-time model caching.

    // old
    public class DynamicModelCacheKeyFactoryDesignTimeSupport : IModelCacheKeyFactory
    {
       public object Create(DbContext context) => 
         context is DynamicContext dynamicContext
           ? (context.GetType(), dynamicContext.UseIntProperty)
           : (object)context.GetType();

        public object Create(DbContext context) => Create(context, false);
    }

    // new
    public class DynamicModelCacheKeyFactoryDesignTimeSupport : IModelCacheKeyFactory
    {
       public object Create(DbContext context, bool designTime) => 
         context is DynamicContext dynamicContext
           ? (context.GetType(), dynamicContext.UseIntProperty, designTime)
           : (object)context.GetType();

        public object Create(DbContext context) => Create(context, false);
    }

### Nested optional dependents with no required properties

> Entity type '[EntityType]' is an optional dependent using table sharing and
> containing other dependents without any required non shared property to
> identify whether the entity exists. If all nullable properties contain a null
> value in database then an object instance won't be created in the query
> causing nested dependent's values to be lost. Add a required property to
> create instances with null values for other properties or mark the incoming
> navigation as required to always create an instance.

The message above is a consequence of a [high-impact breaking change][5] introduced
in EF Core 6.0. In the past, you could have models with nested optional dependents
sharing the same table, each with no required properties. In such
circumstances, data loss could occur (see the [documentation][5] for details
and examples). My solution was to mark at least one property of dependent
models with the `RequiredAttribute` (which, in every single case, was the right
thing to do anyway)

### The `EFCore.NamingConventions` package is missing a method

> Method 'GetServiceProviderHashCode' in type 'ExtensionInfo' from assembly
> 'EFCore.NamingConventions"

The message says it all: there's currently a missing method in the latest
stable version of the `EFCore.NamingConventions` package. At the time of this
writing, `v6.0` of the package has not been released, but there is a pre-release
available that includes the missing implementation. Switch to `v6.0.0-rc.1` and
you'll be fine (ticket is [here][6]). I'm sure the new stable release will be
out by the time you read this.

*Update: EFCore.NamingConventions v6 has now been released.*

### The Npgsql timestamps breaking change 

While the above situations were quick to fix, the new, updated Npgsql provider
offers a different threat level. There's [one significant breaking change][7]
that impacts `DateTime` fields (timestamps). As the documentation suggests, it is
possible to opt out of this change to preserve backward compatibility, but
I decided to take the plunge and embrace it. The short version is that
Postgres's `timestamp` fields ('timestamps without timezone') are changed to
`timestampz` ('timestamps with time zones'). In the application, when dealing
with Npgsql, `DateTime` properties must be treated as UTC by setting the `Kind`
property to `DateTimeKind.UTC`. When you run the migration tool, a migration is
created to accomodate the change, which can impact existing data. Make sure you
read the [detailed notes][8] to assess the impact on your data. I let the
migration run, then updated models configuration by setting a custom
`DateTimeUtcValueConverter` for DateTime properties:

    // custom DateTime converter
    protected readonly ValueConverter DateTimeToUtcConverter = 
      new ValueConverter<DateTime, DateTime>(
        v => DateTime.SpecifyKind(v, DateTimeKind.Utc),
        v => v);

    // Entity configuration 
    internal class MyEntityConfiguratin : IEntityTypeConfiguration<MyEntity> 
    {
      public override void Configure(EntityTypeBuilder<MyEntity> builder)
      {
        builder.Property(o => o.Date).HasConversion(DateTimeToUtcConverter);
      }
    }

Now Postgres timestamps are stored as 'timestamp with timezone (timestampz).
Actual values are UTC as before. A custom converter is attached to the `Date`
property at the application level to ensure that values are correctly handled.

Our stack is now fully running on .NET 6. Upgrading a standard ASP.NET
5 project to .NET 6 revealed to be relatively straightforward. The EF Core
6.0 migration can be more involved, while the Npgsql 6 migration requires some
attention but, remember, you can always opt-out of the delicate timestamps
change. Was the upgrade worth it? I think so for a few reasons. First, .NET
6 is LTS, while .NET 5 will be out of support in six months. Second, .[NET 6 is
the fastest yet][9], with a remarkable margin (EF Core 6 alone is [70%
faster][10].) While the primary migration is done, there are a lot of changes
and new features that are worth considering for our codebase, which is
something we will be doing in the upcoming weeks.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or follow @[nicolaiarocci][tw] on Twitter*

 [1]: https://docs.microsoft.com/en-us/aspnet/core/migration/50-to-60
 [2]: https://docs.microsoft.com/en-us/dotnet/core/compatibility/serialization/6.0/jsonserializer-source-generator-overloads
 [3]: https://docs.microsoft.com/en-us/dotnet/fundamentals/syslib-diagnostics/syslib0023
 [4]: https://github.com/dotnet/EntityFramework.Docs/pull/3305/files
 [5]: https://docs.microsoft.com/en-us/ef/core/what-is-new/ef-core-6.0/breaking-changes#high-impact-changes
 [6]: https://github.com/efcore/EFCore.NamingConventions/issues/108
 [7]: https://www.npgsql.org/efcore/release-notes/6.0.html#major-changes-to-timestamp-mapping
 [8]: https://www.npgsql.org/efcore/release-notes/6.0.html#migrating-columns-from-timestamp-to-timestamptz
 [9]: https://devblogs.microsoft.com/dotnet/announcing-net-6
 [10]: https://docs.microsoft.com/en-us/ef/core/what-is-new/ef-core-6.0/whatsnew#improved-performance-on-techempower-fortunes
 [^11]: My initial ramblings on Minimal APIs are available [here](/will-.net-6-minimal-apis-turn-heads/).
 [rss]: https://nicolaiarocci.com/index.xml
 [tw]: http://twitter.com/nicolaiarocci
 [nl]: https://buttondown.email/nicolaiarocci
