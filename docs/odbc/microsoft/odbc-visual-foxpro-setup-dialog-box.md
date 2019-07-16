---
title: Finestra di dialogo Configurazione ODBC Visual FoxPro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9aa8954cd42ac715b3e6e67e0b0add69d07a570
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915658"
---
# <a name="odbc-visual-foxpro-setup-dialog-box"></a>Finestra di dialogo di configurazione ODBC Visual FoxPro
Il **programma di installazione di ODBC Visual FoxPro** nella finestra di dialogo consente di aggiungere o modificare un'origine dati Visual FoxPro.  
  
 Per scaricare il driver, vedere [sito di download di Driver ODBC Visual FoxPro](https://go.microsoft.com/fwlink/?LinkId=121318).  
  
## <a name="dialog-box-options"></a>Opzioni della finestra di dialogo  
 **Nome dell'origine dati**  
 Digitare il nome da usare per l'origine dati.  
  
 **Descrizione**  
 Digitare una descrizione per l'origine dati.  
  
 **Tipo di database**  
 Consente di scegliere il tipo di database di che cui l'origine dati a cui connettersi.  
  
 **Database di Visual FoxPro (. A DUE BYTE)**  
 Specifica che l'origine dati si connette a un Visual FoxPro [database](../../odbc/microsoft/visual-foxpro-terminology.md) (DBC file) e a tutte le tabelle e viste locali nel database.  
  
 **Directory di tabella disponibili**  
 Specifica che l'origine dati si connette a una directory dei [libero tabelle](../../odbc/microsoft/visual-foxpro-terminology.md). Eventuali [database](../../odbc/microsoft/visual-foxpro-terminology.md) tabelle nella stessa directory vengono ignorate da funzioni di catalogo ODBC, ad esempio [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md) oppure [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md). Le tabelle del database sono accessibili tramite istruzioni SQL SELECT inviate tramite [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md) e [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md).  
  
 **Percorso**  
 Visualizza il percorso e il nome per il database o la directory delle tabelle gratuite a cui si connette l'origine dati.  
  
 **Sfoglia**  
 Consente di ricercare il sistema e la rete per il database o la directory a cui si desidera connettersi all'origine dati.  
  
 **Opzioni**  
 Espande la finestra di dialogo in modo che è possibile impostare le opzioni di Driver ODBC Visual FoxPro.  
  
## <a name="driver"></a>Driver  
 **Sequenza di ordinamento**  
 La sequenza nella quale vengono ordinati i campi. Le sequenze predefinite riflettono le sequenze supportate dalla versione del linguaggio del sistema operativo. Per un elenco di sequenze di collazione supportati, vedere [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
 **Exclusive**  
 Quando questa casella di controllo è selezionata, il driver consente di aprire il database di Visual FoxPro esclusivamente quando si accede ai dati usando l'origine dati. Ad altri utenti non è possibile accedere al database o le tabelle nel database mentre il database è aperto in modo esclusivo. Le tabelle all'interno del database in modo esclusivo aperta vengono aperti come condiviso. Per aprire una tabella in modo esclusivo, utilizzare il [SET esclusivo](../../odbc/microsoft/set-exclusive-command.md) comando. Questa casella di controllo è disabilitata quando **tipo di Database** è impostata su **directory gratuita tabella**.  
  
 **Null**  
 Determina se le colonne create con ALTER TABLE e CREATE TABLE consentono valori null. Se è impostata su ON Null, INSERT - SQL, che inserisce un valore null in qualsiasi colonna non inclusa in un'istruzione INSERT - SQL... Clausola VALUE. Se Null corrisponde a OFF, viene inserito uno spazio vuoto. È inoltre possibile controllare questa opzione in una stringa di connessione passata come nel codice seguente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;NULL=NO"  
```  
  
 **Eliminato**  
 Determina se vengono restituite righe contrassegnate come eliminate. È inoltre possibile controllare questa opzione in una stringa di connessione passata come nel codice seguente:  
  
```  
strCon = "DRIVER=MICROSOFT VISUAL FOXPRO DRIVER;  
SOURCETYPE=DBC;SOURCEDB=D:\Testdata.dbc;BACKGROUNDFETCH=NO;  
DELETED=YES"  
```  
  
 **Recuperare i dati in background**  
 Determina se i record verranno recuperati in background (recupero progressivo) o l'applicazione resta in attesa finché vengono recuperati tutti i record nel set di risultati.
