---
description: Installazione di SMO (SQL Server Management Objects)
title: Installazione di SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 15ce6ea1c72bee64ad8fe96e70b9a7c513c623e6
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868276"
---
# <a name="installing-smo"></a>Installazione di SMO (SQL Server Management Objects)

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

In questa pagina vengono fornite informazioni su come installare SMO per l'utilizzo da parte delle applicazioni e i requisiti di sistema per l'utilizzo di SMO.

## <a name="smo-nuget-package"></a>Pacchetto NuGet SMO

A partire da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO viene distribuito come pacchetto NuGet [Microsoft. SqlServer. SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) per consentire agli utenti di sviluppare applicazioni con Smo.

Si tratta di una sostituzione per SharedManagementObjects.msi, che è stata precedentemente rilasciata come parte del Feature Pack di SQL per ogni versione di SQL Server. Le applicazioni che usano SMO devono essere aggiornate in modo da usare il pacchetto NuGet e saranno responsabili della verifica dell'installazione dei file binari con l'applicazione in fase di sviluppo.

>>[!Important]
>>Come indicato nella pagina [file e numeri di versione](files-and-version-numbers.md) , è consigliabile non installare gli assembly SMO nella global assembly cache (GAC). Questa operazione potrebbe causare problemi con altre applicazioni che utilizzano anche le versioni di SMO, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio.

## <a name="installing-the-package"></a>Installazione del pacchetto

Vedere [NuGet avvio rapido: usare un pacchetto](/nuget/quickstart/use-a-package) per istruzioni ed esempi di installazione e uso di un pacchetto NuGet. 
  
## <a name="system-requirements"></a>Requisiti di sistema
  
 SMO richiede [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] l'esecuzione di 4,0 o .NET Core 2,0, pertanto tutte le applicazioni che lo utilizzano devono assicurarsi che i computer client dispongano di tale versione o versione successiva. Alcuni file binari nativi installati con le librerie SMO NetFx richiedono anche l'installazione del runtime VC 2013; il runtime non è incluso nel pacchetto. È possibile scaricare il redist appropriato per l'architettura di destinazione da https://www.microsoft.com/download/details.aspx?id=40784
