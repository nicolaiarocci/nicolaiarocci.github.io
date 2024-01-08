---
title: Cancellare tutte le Tabelle da un Database SQL Server
author: Nicola Iarocci
date: 2011-03-09
url: /cancellare-tutte-le-tabelle-da-un-database-sql-server/
dsq_thread_id:
  - 2017455376
categories:
  - Guide
  - Programming
tags:
  - sql
  - sql server
---
In rari casi può capitare la necessità di cancellare tutto, ma proprio tutto, da un database SQL Server. **Tabelle**, **Stored Procedure**, **Funzioni**, **Viste**, **Relazioni** e **Chiavi Primarie**. A questo punto tanto varrebbe cancellare il database e ricrearlo, direte voi. Vero, ma non sempre si dispone delle autorizzazioni per farlo. Nel mio caso si tratta di un database ospitato su un server remoto e condiviso. Posso creare e cancellare quel che voglio all&#8217;interno del database, ma non posso rinominare o cancellare il db stesso.<!--more-->

Ecco una [comoda routine][1] che fa al caso nostro. Dopo averla eseguita vi troverete il database completamente vuoto, come se fosse stato appena creato.

<pre>/* Drop di tutte le Stored Procedure che non siano di sistema */
DECLARE @name VARCHAR(128)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'P' AND category = 0 ORDER BY [name])

WHILE @name is not null
BEGIN
    SELECT @SQL = 'DROP PROCEDURE [dbo].[' + RTRIM(@name) +']'
    EXEC (@SQL)
    PRINT 'Cancellata Procedura: ' + @name
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'P' AND category = 0 AND [name] &gt; @name ORDER BY [name])
END
GO

/* Drop di tutte le viste */
DECLARE @name VARCHAR(128)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'V' AND category = 0 ORDER BY [name])

WHILE @name IS NOT NULL
BEGIN
    SELECT @SQL = 'DROP VIEW [dbo].[' + RTRIM(@name) +']'
    EXEC (@SQL)
    PRINT 'Cancellata Vista: ' + @name
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'V' AND category = 0 AND [name] &gt; @name ORDER BY [name])
END
GO

/* Drop di tutte le funzioni */
DECLARE @name VARCHAR(128)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] IN (N'FN', N'IF', N'TF', N'FS', N'FT') AND category = 0 ORDER BY [name])

WHILE @name IS NOT NULL
BEGIN
    SELECT @SQL = 'DROP FUNCTION [dbo].[' + RTRIM(@name) +']'
    EXEC (@SQL)
    PRINT 'Cancellata la Funzione: ' + @name
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] IN (N'FN', N'IF', N'TF', N'FS', N'FT') AND category = 0 AND [name] &gt; @name ORDER BY [name])
END
GO

/* Cancella tutti i vincoli di Foreign Key */
DECLARE @name VARCHAR(128)
DECLARE @constraint VARCHAR(254)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' ORDER BY TABLE_NAME)

WHILE @name is not null
BEGIN
    SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)
    WHILE @constraint IS NOT NULL
    BEGIN
        SELECT @SQL = 'ALTER TABLE [dbo].[' + RTRIM(@name) +'] DROP CONSTRAINT ' + RTRIM(@constraint)
        EXEC (@SQL)
        PRINT 'Cancallato Vincolo FK: ' + @constraint + ' on ' + @name
        SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' AND CONSTRAINT_NAME &lt;&gt; @constraint AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)
    END
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'FOREIGN KEY' ORDER BY TABLE_NAME)
END
GO

/* Cancella i vincoli Primary Key */
DECLARE @name VARCHAR(128)
DECLARE @constraint VARCHAR(254)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' ORDER BY TABLE_NAME)

WHILE @name IS NOT NULL
BEGIN
    SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)
    WHILE @constraint is not null
    BEGIN
        SELECT @SQL = 'ALTER TABLE [dbo].[' + RTRIM(@name) +'] DROP CONSTRAINT ' + RTRIM(@constraint)
        EXEC (@SQL)
        PRINT 'Cancellato Vincolo PK: ' + @constraint + ' on ' + @name
        SELECT @constraint = (SELECT TOP 1 CONSTRAINT_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' AND CONSTRAINT_NAME &lt;&gt; @constraint AND TABLE_NAME = @name ORDER BY CONSTRAINT_NAME)
    END
SELECT @name = (SELECT TOP 1 TABLE_NAME FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS WHERE constraint_catalog=DB_NAME() AND CONSTRAINT_TYPE = 'PRIMARY KEY' ORDER BY TABLE_NAME)
END
GO

/* Drop di tutte le Tabelle */
DECLARE @name VARCHAR(128)
DECLARE @SQL VARCHAR(254)

SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'U' AND category = 0 ORDER BY [name])

WHILE @name IS NOT NULL
BEGIN
    SELECT @SQL = 'DROP TABLE [dbo].[' + RTRIM(@name) +']'
    EXEC (@SQL)
    PRINT 'Cancellata Tabella: ' + @name
    SELECT @name = (SELECT TOP 1 [name] FROM sysobjects WHERE [type] = 'U' AND category = 0 AND [name] &gt; @name ORDER BY [name])
END
GO
</pre>

Anche questa routine (come [quella vista ieri che cancella le sole Stored Procedure][2]) accede alla tabella di sistema `sys.objects` per reperire lo schema del database. Cambia però la tecnica di accesso alle informazioni. Invece di usare un cursore qui selezioniamo il primo record utile per poi inoltrarci in un ciclo di cancellazioni ripetute. Il ciclo termina quando non ci sono più record che soddisfano i parametri di ricerca. Per evitare problemi coi vincoli relazionali è importante cancellare prima le relazioni e solo dopo le tabelle.

## Nota Bene

Probabilmente c&#8217;è una ottima ragione per cui non disponete dei diritti di cancellazione del database. Prima di lanciare questo codice chiedetevi almeno dieci volte se 1) state sul database giusto, 2) siete coscienti delle conseguenze di quel che state per fare e 3) disponete di un backup dei dati. In ogni caso se perdete dati preziosi **non venite a lamentarvi dal sottoscritto! 😉**

 [1]: http://stackoverflow.com/questions/536350/sql-server-2005-drop-all-the-tables-stored-procedures-triggers-constriants-an
 [2]: http://nicolaiarocci.com/come-rimuovere-tutte-le-stored-procedure-da-un-database-sql/
