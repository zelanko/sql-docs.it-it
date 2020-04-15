---
title: Finestra di dialogo Installazione di ODBC Visual FoxPro - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], installing
- FoxPro ODBC driver [ODBC], installing
ms.assetid: de020197-7f53-4643-9cbf-b7887ba88de9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef7ac702a69342833c6dfffa0ffc9cdd0ac2857e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298081"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Finestra di dialogo di configurazione ODBC Visual FoxPro
La finestra di dialogo **Installazione di ODBC Visual FoxPro** consente di aggiungere o modificare un'origine dati Visual FoxPro.  
  
 Per scaricare il driver, vedere il sito di [download del driver ODBC di Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opzioni della finestra di dialogo  
 **Nome origine dati**  
 Digitare il nome che si desidera utilizzare per l'origine dati.  
  
 **Descrizione**  
 Digitare una descrizione per l'origine dati.  
  
 **Tipo di database**  
 Consente di scegliere il tipo di database a cui si desidera connettere l'origine dati.  
  
 **Database di Visual FoxPro (. DBC)**  
 Specifica che l'origine dati si connette a un [database](../../odbc/microsoft/visual-foxpro-terminology.md) Visual FoxPro (file con estensione dbc) e a tutte le tabelle e le viste locali del database.  
  
 **Directory tabella libera**  
 Specifica che l'origine dati si connette a una directory di [tabelle libere.](../../odbc/microsoft/visual-foxpro-terminology.md) Tutte le tabelle di [database](../../odbc/microsoft/visual-foxpro-terminology.md) nella stessa directory vengono ignorate dalle funzioni di catalogo ODBC, ad esempio [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) o [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). È possibile accedere alle tabelle di database utilizzando le istruzioni SQL SELECT inviate tramite [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Percorso**  
 Visualizza il percorso e il nome del database o la directory delle tabelle libere a cui si connette l'origine dati.  
  
 **Sfoglia**  
 Consente di cercare nel sistema e nella rete il database o la directory a cui si desidera connettere l'origine dati.  
  
 **Opzioni**  
 Espande la finestra di dialogo in modo che sia possibile impostare le opzioni del driver ODBC di Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequenza di confronto**  
 Sequenza di ordinamento dei campi. Le sequenze predefinite riflettono le sequenze supportate dalla versione in lingua del sistema operativo. Per un elenco delle sequenze di confronto supportate, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando questa casella di controllo è selezionata, il driver apre il database di Visual FoxPro esclusivamente quando si accede ai dati utilizzando l'origine dati. Gli altri utenti non possono accedere al database o alle tabelle del database mentre il database è aperto in modo esclusivo. Le tabelle all'interno del database aperto in modo esclusivo vengono aperte come CONDIVIDI. Per aprire una tabella in modo esclusivo, utilizzare il comando [SET EXCLUSIVE.](../../odbc/microsoft/set-exclusive-command.md) Questa casella di controllo è disabilitata quando **Tipo di database** è impostato su Directory tabella **libera**.  
  
 **Null**  
 Determina se le colonne create con ALTER TABLE e CREATE TABLE consentono valori Null. Se si imposta Null ON, INSERT - SQL inserisce un valore null in qualsiasi colonna non inclusa in un'istruzione INSERT - SQL... Clausola VALUE. Se Null è OFF, viene inserito uno spazio vuoto. È anche possibile controllare questa opzione tramite una stringa di connessione passata come nel codice seguente:You can also control this option through a passed connection string as in the following code:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminato**  
 Determina se vengono restituite le righe contrassegnate come eliminate. È anche possibile controllare questa opzione tramite una stringa di connessione passata come nel codice seguente:You can also control this option through a passed connection string as in the following code:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Recuperare i dati in background**  
 Determina se i record verranno recuperati in background (recupero progressivo) o se l'applicazione attenderà fino al recupero di tutti i record nel set di risultati.
