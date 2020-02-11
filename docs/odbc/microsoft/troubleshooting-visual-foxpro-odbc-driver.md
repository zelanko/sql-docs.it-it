---
title: Risoluzione dei problemi (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI [ODBC]
- troubleshooting Visual FoxPro ODBC driver [ODBC]
- remote views [ODBC]
- multitiered views [ODBC]
- parameterized views [ODBC], Visual FoxPro ODBC driver
- fetches [ODBC], Visual FoxPro ODBC driver
- positioned updates [ODBC]
- background fetching [ODBC]
ms.assetid: fd478dd8-666a-4f0a-a2d6-b94e81cbbe4b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4eeb6210b9bce124e16a1b4e666dee03c1d992be
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912379"
---
# <a name="troubleshooting-visual-foxpro-odbc-driver"></a>Risoluzione dei problemi (driver ODBC Visual FoxPro)
Nelle sezioni seguenti viene illustrato come migliorare le prestazioni e risolvere i problemi che possono verificarsi durante l'utilizzo del driver ODBC Visual FoxPro.  
  
## <a name="accessing-parameterized-views"></a>Accesso alle viste con parametri  
 Non è possibile accedere alle viste con parametri in un database Visual FoxPro usando il driver. Una vista con parametri crea una clausola WHERE nell'istruzione SQL **Select** della vista che limita i record scaricati nei record che soddisfano le condizioni della clausola WHERE compilata usando il valore fornito per il parametro. Poiché il driver non supporta il passaggio di parametri alla visualizzazione, i tentativi di accesso a una vista con parametri tramite il driver avranno esito negativo.  
  
 Il valore del parametro può essere specificato in fase di esecuzione o passato a livello di codice alla vista.  
  
## <a name="accessing-remote-views"></a>Accesso alle viste remote  
 Non è possibile accedere alle viste remote in un database Visual FoxPro usando il driver. Le visualizzazioni remote sono viste che accedono a dati non FoxPro o a una combinazione di dati FoxPro e non FoxPro. Per accedere alle visualizzazioni remote, usare Visual FoxPro.  
  
## <a name="deleting-records"></a>Eliminazione di record  
 È possibile contrassegnare i record per l'eliminazione usando il driver, ma non è possibile rimuovere definitivamente i record dal database. Per rimuovere definitivamente i record da una tabella, usare Visual FoxPro.  
  
## <a name="increasing-performance-using-background-fetching"></a>Miglioramento delle prestazioni tramite il recupero in background  
 È possibile migliorare le prestazioni per operazioni di recupero di grandi dimensioni utilizzando la funzionalità di recupero in background del driver. Il recupero in background usa un thread separato per recuperare i dati richiesti da un'origine dati specifica.  
  
 È possibile utilizzare il recupero in background per un'origine dati in uno dei modi seguenti:  
  
-   Selezionare la casella **di controllo Recupera dati in background** nella finestra di [dialogo di installazione di ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md).  
  
-   Usare la parola chiave dell'attributo BackgroundFetch nella stringa di connessione.  
  
 Per informazioni sulle parole chiave degli attributi della stringa di connessione, vedere [utilizzo delle stringhe di connessione](../../odbc/microsoft/using-connection-strings.md).  
  
## <a name="updating-multitiered-views"></a>Aggiornamento di viste a più livelli  
 Una vista a più livelli è una vista basata su una o più visualizzazioni anziché su una tabella di base. Quando si aggiornano i dati in una visualizzazione a più livelli, gli aggiornamenti diventano inattivi di un solo livello, fino alla visualizzazione sulla quale è basata la visualizzazione di primo livello. le tabelle di base non vengono aggiornate.  
  
## <a name="using-data-definition-language-ddl-in-stored-procedures"></a>Utilizzo di DDL (Data Definition Language) nelle stored procedure  
 Non è possibile usare DDL, ad esempio CREATE TABLE o ALTER TABLE, nelle stored procedure di Visual FoxPro.  
  
 Per informazioni sul linguaggio che è possibile utilizzare nelle stored procedure, vedere [supporto per regole, trigger, valori predefiniti e stored procedure](../../odbc/microsoft/support-rules-triggers-defaults-stored-procedures-visual-foxpro-odbc-driver.md).  
  
## <a name="using-positioned-updates"></a>Uso degli aggiornamenti posizionati  
 Il driver non supporta gli aggiornamenti posizionati. Utilizzare la clausola SQL WHERE per identificare le righe che si desidera aggiornare.  
  
## <a name="using-the-set-ansi-command"></a>Uso del comando SET ANSI  
 Se si è uno sviluppatore Visual FoxPro, è necessario tenere presente che l'impostazione predefinita per SET ANSI è ON per il driver, a differenza dell'impostazione predefinita OFF per Visual FoxPro. L'impostazione predefinita ON per SET ANSI consente alle origini dati Visual FoxPro di comportarsi in modo coerente con altre origini dati ODBC che in genere eseguono confronti esatti. È possibile modificare l'impostazione predefinita. Per ulteriori informazioni, vedere [set ANSI](../../odbc/microsoft/set-ansi-command.md).
