---
title: Trasformazione Cache | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.cachetrans.f1
- sql13.dts.designer.cachetranscon.f1
- sql13.dts.designer.cachetransmap.f1
helpviewer_keywords:
- Cache transform
ms.assetid: a5683fc8-9c32-4634-819e-e9815627e4f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b9fc1882dec5946e002d906afc07541d0923fc18
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922492"
---
# <a name="cache-transform"></a>trasformazione Cache

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  La trasformazione Cache genera un set di dati di riferimento per la trasformazione Ricerca mediante la scrittura di dati da un'origine dati connessa nel flusso di dati a una gestione connessione cache. La trasformazione Ricerca esegue ricerche unendo in join i dati contenuti nelle colonne di input da un'origine dati connessa con le colonne nel database di riferimento.  
  
 È possibile utilizzare la gestione connessione Cache quando si desidera configurare la trasformazione Ricerca per l'esecuzione in modalità Full Cache. In questa modalità, il set di dati di riferimento viene caricato nella cache prima dell'esecuzione della trasformazione Ricerca.  
  
 Per istruzioni su come configurare la trasformazione Ricerca in modalità Full Cache utilizzando la gestione connessione cache e una trasformazione Cache, vedere [Implementazione di una trasformazione Ricerca in modalità Full Cache utilizzando la gestione connessione della cache](../../../integration-services/data-flow/transformations/lookup-transformation-full-cache-mode-cache-connection-manager.md).  
  
 Per ulteriori informazioni sulla memorizzazione nella cache del set di dati di riferimento, vedere [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
> [!NOTE]  
>  La Trasformazione cache scrive solo righe univoche nella gestione connessione della cache.  
  
 In un pacchetto singolo, solo una trasformazione Cache può scrivere i dati nella stessa gestione connessione della cache. Se il pacchetto contiene più trasformazioni Cache, la prima ad essere chiamata quando il pacchetto viene eseguito è quella che scrive i dati nella gestione connessione. Le operazioni di scrittura delle trasformazioni Cache successive non vengono eseguite.  
  
 Per altre informazioni, vedere [Gestione connessione della cache](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
## <a name="configuration-of-the-cache-transform"></a>Configurazione della trasformazione Cache  
 È possibile configurare la gestione connessione della cache in modo da salvare i dati in un file di cache (con estensione caw).  
  
 Per configurare la trasformazione Cache, procedere nel modo seguente:  
  
-   Specificare la gestione connessione della cache.  
  
-   Eseguire il mapping delle colonne di input nella trasformazione Cache alle colonne di destinazione nella gestione connessione della cache.  
  
    > [!NOTE]  
    >  È necessario eseguire il mapping di ogni colonna di input a una colonna di destinazione e i tipi di dati di colonna devono corrispondere. In caso contrario, in Progettazione [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] viene visualizzato un messaggio di errore.  
  
     È possibile utilizzare **Editor gestione connessione della cache** per modificare i tipi di dati, i nomi e altre proprietà delle colonne.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** , vedere [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="cache-transformation-editor-connection-manager-page"></a>Editor trasformazione cache (pagina Gestione connessioni)
  Utilizzare la scheda **Gestione connessione** della finestra di dialogo **Editor trasformazione cache** per selezionare una gestione connessione esistente o crearne una nuova.  
  
 Per ulteriori informazioni sulla gestione connessione cache, vedere [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Gestione connessione della cache**  
 Consente di selezionare una gestione connessione della cache esistente utilizzando l'elenco o di creare una nuova connessione usando il pulsante **Nuova** .  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione nella finestra di dialogo Editor gestione connessione cache.  
  
 **Modifica**  
 Consente di modificare una connessione esistente.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)  
  
  
