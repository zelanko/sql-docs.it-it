---
title: Connessione a origini dati nel componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], connecting to data sources
ms.assetid: 96de63ab-ff48-4e7e-89e0-ffd6a89c63b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 82ec2ddf98780a7230ccc123e3de152ad643669a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296967"
---
# <a name="connecting-to-data-sources-in-the-script-component"></a>Connessione a origini dati nel componente script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione è un'unità pratica che incapsula e archivia le informazioni necessarie per la connessione a un'origine dati di un determinato tipo. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
 È possibile rendere disponibili le gestioni connessioni esistenti per l'accesso da parte dello script personalizzato nel componente di origine o destinazione facendo clic sui pulsanti **Aggiungi** e **Rimuovi** nella pagina **Gestioni connessioni** dell'**Editor trasformazione Script**. È tuttavia necessario scrivere codice personalizzato per caricare o salvare i dati e possibilmente per aprire e chiudere la connessione all'origine dati. Per altre informazioni sulla pagina **Gestioni connessioni** dell'**Editor trasformazione Script**, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md) ed [Editor trasformazione Script &#40;pagina Gestioni connessioni&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md).  
  
 Il componente script crea una classe di raccolta **Connections** nell'elemento di progetto **ComponentWrapper** che contiene una funzione di accesso fortemente tipizzata per ogni gestione connessione che ha lo stesso nome della gestione connessione. Questa raccolta viene esposta tramite la proprietà **Connections** della classe **ScriptMain**. La proprietà della funzione di accesso restituisce un riferimento alla gestione connessione come istanza di <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Ad esempio, se è stata aggiunta una gestione connessione denominata `MyADONETConnection` nella pagina Gestioni connessioni della finestra di dialogo, è possibile ottenere un riferimento ad essa nello script tramite il codice seguente:  
  
 `Dim myADONETConnectionManager As IDTSConnectionManager100 = _`  
  
 `Me.Connections.MyADONETConnection`  
  
> [!NOTE]  
>  È necessario conoscere il tipo di connessione restituito dalla gestione connessione prima di chiamare **AcquireConnection**. Poiché l'oggetto **Option Strict** dell'attività Script è abilitato, è necessario eseguire il cast della connessione, che viene restituita come tipo **Object**, nel tipo di connessione appropriato prima dell'utilizzo.  
  
 Chiamare quindi il metodo **AcquireConnection** della gestione connessione specifica per ottenere la connessione sottostante o le informazioni necessarie per connettersi all'origine dati. Ad esempio, per ottenere un riferimento a **System.Data.SqlConnection** incluso in una gestione connessione ADO.NET, usare il codice seguente:  
  
 `Dim myADOConnection As SqlConnection = _`  
  
 `CType(MyADONETConnectionManager.AcquireConnection(Nothing), SqlConnection)`  
  
 Viceversa, la stessa chiamata a una gestione connessione file flat restituisce solo il percorso e il nome di file dell'origine dati del file.  
  
 `Dim myFlatFile As String = _`  
  
 `CType(MyFlatFileConnectionManager.AcquireConnection(Nothing), String)`  
  
 È quindi necessario specificare questo percorso e questo nome di file in un oggetto **System.IO.StreamReader** o **Streamwriter** per leggere o scrivere i dati nel file flat.  
  
> [!IMPORTANT]  
>  Quando si scrive codice gestito in un componente script, non è possibile chiamare il metodo AcquireConnection delle gestioni connessioni che restituiscono oggetti non gestiti, ad esempio la gestione connessione OLE DB e la gestione connessione Excel. È tuttavia possibile leggere la proprietà ConnectionString di queste gestioni connessioni e connettersi direttamente all'origine dati nel codice usando la stringa di connessione di un oggetto **connection** OLEDB dallo spazio dei nomi **System.Data.OleDb**.  
>   
>  Se è necessario chiamare il metodo AcquireConnection di una gestione connessione che restituisce un oggetto non gestito, usare una gestione connessione ADO.NET. Quando si configura la gestione connessione ADO.NET per l'utilizzo di un provider OLE DB, la connessione viene eseguita tramite il provider di dati .NET Framework per OLE DB. In questo caso il metodo AcquireConnection restituisce un oggetto **System.Data.OleDb.OleDbConnection** invece di un oggetto non gestito. Per configurare una gestione connessione ADO.NET per l'utilizzo con un'origine dati Excel, selezionare il provider Microsoft OLE DB per Jet, specificare una cartella di lavoro di Excel, quindi immettere `Excel 8.0` (per Excel 97 e versioni successive) come valore di **Proprietà estese** nella pagina **Tutte** della finestra di dialogo **Gestione connessione**.  
  
 Per altre informazioni sull'uso delle gestioni connessioni con il componente script, vedere [Creazione di un'origine con il componente script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md) e [Creazione di una destinazione con il componente script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessioni in Integration Services &#40;SSIS&#41;](../../../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Creare gestioni connessioni](https://msdn.microsoft.com/library/6ca317b8-0061-4d9d-b830-ee8c21268345)  
  
  
