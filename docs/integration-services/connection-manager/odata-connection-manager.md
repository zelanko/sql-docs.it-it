---
title: Gestione connessione OData | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2026e33a9e31f437615e8270c61681ec95b287b2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728114"
---
# <a name="odata-connection-manager"></a>Gestione connessione OData

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 Connettersi a un'origine dati OData con una gestione connessione OData. Un componente di origine OData usa una gestione connessione OData per connettersi a un'origine OData e utilizzare i dati del servizio. Per ulteriori informazioni, vedere [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Aggiunta di una gestione connessione OData a un pacchetto SSIS  
 È possibile aggiungere una nuova gestione connessione OData a un pacchetto SSIS in tre modi:  
  
-   Fare clic sul pulsante **Nuovo...** in **Editor origine OData**  
  
-   Fare clic con il pulsante destro del mouse sulla cartella **Gestioni connessioni** in **Esplora soluzioni**e quindi fare clic su **Nuova gestione connessione**. Selezionare **ODATA** per **Tipo gestione connessione**.  
  
-   Fare clic con il pulsante destro del mouse nel riquadro **Gestioni connessioni** nella parte inferiore della finestra di progettazione del pacchetto e quindi selezionare **Nuova connessione**. Selezionare **ODATA** per **Tipo gestione connessione**.  
  
## <a name="connection-manager-authentication"></a>Autenticazione di gestione connessione  
 La gestione connessione OData supporta cinque modalità di autenticazione.  
  
-   Autenticazione di Windows  
  
-   Autenticazione di base (con il nome utente e la password)  

-   Microsoft Dynamics AX Online (con nome utente e password)
  
-   Microsoft Dynamics CRM Online (con nome utente e password)
  
-   Microsoft Online Services (con nome utente e password)  
  
Per l'accesso anonimo, selezionare l'opzione Autenticazione di Windows.  

Per connettersi a Microsoft Dynamics AX Online o a Microsoft Dynamics CRM Online, non è possibile usare l'opzione di autenticazione **Microsoft Online Services**. Non è neanche possibile usare opzioni configurate per l'autenticazione a più fattori.
  
### <a name="specifying-and-securing-credentials"></a>Specifica e protezione delle credenziali  
 Se il servizio OData richiede l'autenticazione di base, è possibile specificare un nome utente e una password in [Editor gestione connessione OData](../../integration-services/connection-manager/odata-connection-manager-editor.md). I valori immessi nell'editor sono persistenti nel pacchetto. Il valore della password è crittografato in base al livello di protezione del pacchetto.  
  
 È possibile impostare i parametri dei valori del nome utente e della password in più modalità oppure archiviarli all'esterno del pacchetto. È ad esempio possibile usare parametri oppure impostare le proprietà di gestione connessione direttamente quando si esegue il pacchetto da SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Proprietà di gestione connessione OData  
 L'elenco seguente descrive le proprietà di gestione connessione OData.  
  
|||  
|-|-|  
|Proprietà|Descrizione|  
|URL|URL del documento di servizio.|  
|UserName|Nome utente da usare per l'autenticazione, se richiesto.|  
|Password|Password da usare per l'autenticazione, se richiesta.|  
|ConnectionString|Include altre proprietà della gestione connessione.|  
  
## <a name="odata-connection-manager-editor"></a>Editor gestione connessione OData
  Usare la finestra di dialogo **Editor gestione connessione OData** per aggiungere una connessione o modificare una connessione esistente a un'origine dati OData.  
  
### <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Nome della gestione connessione.  
  
 **Percorso documento di servizio**  
 URL del servizio OData. Ad esempio: https://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Autenticazione**  
Selezionare una delle opzioni seguenti:
-   **Autenticazione di Windows**. Selezionare questa opzione per l'accesso anonimo.
-   **Autenticazione di base** 
-   **Microsoft Dynamics AX Online** per Dynamics AX Online
-   **Microsoft Dynamics CRM Online** per Dynamics CRM Online
-   **Microsoft Online Services** per Microsoft Online Services

Se si seleziona un'opzione diversa da Autenticazione di Windows, immettere il **nome utente** e la **password**. 

Per connettersi a Microsoft Dynamics AX Online o a Microsoft Dynamics CRM Online, non è possibile usare l'opzione di autenticazione **Microsoft Online Services**. Non è neanche possibile usare opzioni configurate per l'autenticazione a più fattori.

 **Test connessione**  
 Fare clic su questo pulsante per testare la connessione all'origine OData.  
