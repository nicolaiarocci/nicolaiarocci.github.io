---
date: 2023-03-03T08:05:25+01:00
title: "Making C# and OmniSharp play well with Neovim"
slug: making-csharp-and-omnisharp-play-well-with-neovim
share: false
tags: ["csharp", "neovim", "omnisharp", "programming"]
---
I've recently moved away from my custom Neovim configuration to embrace [LazyVim][1]. LazyVim is a Neovim setup with sane
default settings for options, autocmds, and keymaps. It boldly aims to transform Neovim into a full-fledged IDE that is
easy to extend and customize. It comes with a wealth of plugins pre-configured and ready to use, and it is also blazing
fast. Elijah Manor has a fantastic introductory video on YouTube; I suggest you take the time to look at it.

{{< youtube N93cTbtLCIM >}}
<br/>
So far I'm delighted with the result. In the process, I learned about several useful plugins I now use regularly.

### Neovim trouble with C# and OmniSharp
When I upgraded my old-*ish* Neovim (I am using nightly builds now), I started getting a weird error on every `.cs` file
I loaded: 

````
Error executing vim.schedule lua callbaack: /usr/share/[...]/semantic_tokens.lua:342:E5248: Invalid character in group name.
````

A little investigation revealed that semantic tokens provided by
OmniSharp don't conform to the LSP specification, which triggers the error. I cloned the *omnisharp-roslyn* repo and dug
into the code hoping I could offer a quick fix. As it turns out, however, the issue is actually with [Roslyn
itself][4], not OmniSharp. There are tickets on both the [Neovim][2] and the [OmniSharp][3] repositories, but I fear
they'll stagnate there as non-relevant (*note to self*: maybe report the problem to the Roslyn folks? Alternatively,
propose a patched semantic provider to the *omnisharp-roslyn* maintainers.) 

Anyway, a quick, hacky, and not future-proof fix is to customize Neovim (LazyVim) configuration like this:

```
-- ~/.config/nvim/lua/plugins/omnisharp.lua (create if needed)
return {
  "OmniSharp/omnisharp-vim",
  init = function()
    require("lazyvim.util").on_attach(function(client, _)
      if client.name == "omnisharp" then
        client.server_capabilities.semanticTokensProvider = {
          full = vim.empty_dict(),
          legend = {
            tokenModifiers = { "static_symbol" },
            tokenTypes = {
              "comment",
              "excluded_code",
              "identifier",
              "keyword",
              "keyword_control",
              "number",
              "operator",
              "operator_overloaded",
              "preprocessor_keyword",
              "string",
              "whitespace",
              "text",
              "static_symbol",
              "preprocessor_text",
              "punctuation",
              "string_verbatim",
              "string_escape_character",
              "class_name",
              "delegate_name",
              "enum_name",
              "interface_name",
              "module_name",
              "struct_name",
              "type_parameter_name",
              "field_name",
              "enum_member_name",
              "constant_name",
              "local_name",
              "parameter_name",
              "method_name",
              "extension_method_name",
              "property_name",
              "event_name",
              "namespace_name",
              "label_name",
              "xml_doc_comment_attribute_name",
              "xml_doc_comment_attribute_quotes",
              "xml_doc_comment_attribute_value",
              "xml_doc_comment_cdata_section",
              "xml_doc_comment_comment",
              "xml_doc_comment_delimiter",
              "xml_doc_comment_entity_reference",
              "xml_doc_comment_name",
              "xml_doc_comment_processing_instruction",
              "xml_doc_comment_text",
              "xml_literal_attribute_name",
              "xml_literal_attribute_quotes",
              "xml_literal_attribute_value",
              "xml_literal_cdata_section",
              "xml_literal_comment",
              "xml_literal_delimiter",
              "xml_literal_embedded_expression",
              "xml_literal_entity_reference",
              "xml_literal_name",
              "xml_literal_processing_instruction",
              "xml_literal_text",
              "regex_comment",
              "regex_character_class",
              "regex_anchor",
              "regex_quantifier",
              "regex_grouping",
              "regex_alternation",
              "regex_text",
              "regex_self_escaped_character",
              "regex_other_escape",
            },
          },
          range = true,
        }
      end
    end)
  end,
}

```

It overrides the `on_attach` event to pass an LSP-digestible list of semantic tokens. And voilà, C# files are now loaded seamlessly.

I'm not done yet. I'm having another [weird issue][5] with *.editorconfig* files. I'm still triaging it, and will report back when (if) I sort it out.

*Subscribe to the [newsletter][nl], the [RSS feed][rss], or [follow me on Mastodon][m]*

 [1]: https://www.lazyvim.org/
 [2]: https://github.com/neovim/neovim/issues/21391
 [3]: https://github.com/OmniSharp/omnisharp-roslyn/issues/2483
 [4]: https://github.com/dotnet/roslyn/blob/3cca4fdc3b125995bfd32b3a02b5d5c2d2b82504/src/Workspaces/Core/Portable/Classification/ClassificationTypeNames.cs#L97
 [5]: https://github.com/OmniSharp/omnisharp-roslyn/issues/2510
 [rss]: https://nicolaiarocci.com/index.xml
 [m]: https://fosstodon.org/@nicola
 [nl]: https://buttondown.email/nicolaiarocci
