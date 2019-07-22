---
title: Schermata 1 della creazione guidata origine dati (driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6edf465f5b853008c9bdc8c420f6e862e360593
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936608"
---
# <a name="data-source-wizard-screen-1"></a>Creazione guidata origine dati - Schermata 1

Specificare il nome e la descrizione dell'origine dati e il nome del server in cui viene eseguito SQL Server cui si connetterà l'origine dati. 
    
## <a name="options"></a>Opzioni

### <a name="name"></a>nome

Nome dell'origine dati utilizzato da un'applicazione ODBC quando richiede una connessione all'origine dati, ad esempio "Personale". Il nome dell'origine dati è visualizzato nella finestra di dialogo Amministrazione origine dati ODBC.

### <a name="description"></a>Descrizione

Descrizione facoltativa dell'origine dati, ad esempio "Date collaborazioni, cronologia stipendi e situazione corrente di tutti i dipendenti".

### <a name="select-or-enter-a-server-name"></a>Selezionare o immettere il nome di un server

Nome di un'istanza di SQL Server sulla rete. Sarà necessario specificare un server nella casella di modifica successiva.

Nella maggior parte dei casi, il driver ODBC può connettersi usando l'ordine dei protocolli predefinito e il nome del server specificato in questa casella. Usare Gestione configurazione SQL Server se si vuole creare un alias per il server o configurare librerie di rete client.

È possibile immettere "(locale)" nella casella del server quando si usa lo stesso computer in cui è presente SQL Server. L'utente può quindi connettersi all'istanza locale di SQL Server anche in caso di esecuzione di una versione non in rete di SQL Server. È possibile eseguire più istanze di SQL Server nello stesso computer. Per specificare un'istanza denominata di SQL Server, il nome del server deve essere specificato come _NomeServer_\\_NomeIstanza_.

Per altre informazioni sui nomi dei server per tipi diversi di reti, vedere la documentazione relativa all'installazione di SQL Server nella documentazione online di SQL Server.

### <a name="finish"></a>Fine

Se le informazioni specificate in questa schermata sono le uniche necessarie per connettersi a SQL Server, è possibile fare clic su **Fine**. Per tutti gli attributi specificati nelle altre schermate della procedura guidata verranno utilizzate le impostazioni predefinite.

### <a name="next"></a>Avanti

Per passare alla schermata successiva della procedura guidata, fare clic su **Avanti**.

## <a name="next-steps"></a>Passaggi successivi

[Creazione guidata origine dati - Schermata 2](../../../connect/odbc/windows/dsn-wizard-2.md)
