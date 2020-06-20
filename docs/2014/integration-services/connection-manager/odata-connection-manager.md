---
title: Gestione connessione OData | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3c20d069a419a4d9f95a31489449a4726e25c304
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920457"
---
# <a name="odata-connection-manager"></a>Gestione connessione OData
  Con la gestione connessione OData è possibile connettere un pacchetto a un'origine OData. Tramite un componente di origine OData viene eseguita la connessione a un'origine OData mediante una gestione connessione OData e vengono utilizzati i dati del servizio. Vedere la sezione [origine OData](../data-flow/odata-source.md)per informazioni dettagliate, incluse le istruzioni di installazione per questi componenti.  
  
## <a name="adding-connection-manager-to-an-ssis-package"></a>Aggiunta di gestione connessione a un pacchetto SSIS  
 È possibile aggiungere una nuova gestione connessione OData a un pacchetto SSIS nelle tre modalità seguenti:  
  
-   Fare clic sul pulsante **Nuovo...** in **Editor origine OData**  
  
-   Fare clic con il pulsante destro del mouse sulla cartella **gestioni connessioni** nel **Esplora soluzioni** e scegliere **nuova gestione connessione**. Selezionare **ODATA** per **Tipo gestione connessione**.  
  
-   Fare clic con il pulsante destro del mouse nel riquadro **gestioni connessioni** nella parte inferiore della finestra di progettazione del pacchetto e selezionare **nuova connessione.** Selezionare **OData** per **tipo gestione connessione**.  
  
## <a name="connection-manager-authentication"></a>Autenticazione di gestione connessione  
 La gestione connessione OData supporta due modalità di autenticazione.  
  
-   Autenticazione di Windows  
  
-   Autenticazione di base (nome utente/password)  
  
 Per l'accesso anonimo, selezionare l'opzione Autenticazione di Windows.  
  
### <a name="specifying-and-securing-credentials"></a>Specifica e protezione delle credenziali  
 Se il servizio OData richiede l'autenticazione di base, è possibile specificare un nome utente e una password nell' [Editor gestione connessione OData](../odata-connection-manager-editor.md). I valori immessi nell'editor sono persistenti nel pacchetto. Il valore della password è crittografato in base al livello di protezione del pacchetto.  
  
 È possibile esternalizzare/impostare i parametri dei valori del nome utente e della password in più modalità. Le due modalità principali per eseguire questa operazione in [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)] consistono nell'utilizzo dei parametri oppure nell'impostare le proprietà di gestione connessione direttamente quando si esegue il pacchetto mediante SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Proprietà di gestione connessione OData  
 Nell'elenco seguente vengono descritte alcune delle proprietà di gestione connessione OData che è possibile modificare.  
  
|||  
|-|-|  
|Proprietà|Descrizione|  
|URL|URL del documento di servizio.|  
|UserName|Nome utente da utilizzare per l'autenticazione di base.|  
|Password|Password da utilizzare per l'autenticazione di base.|  
|ConnectionString|Riflette altre proprietà della gestione connessione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Editor gestione connessione OData](../odata-connection-manager-editor.md)  
  
  
