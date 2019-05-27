---
title: Per più file Flat Connection Manager Editor (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6d4b926d08096087735458ed309e5bc4189a87df
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057478"
---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor gestione connessione per più file flat (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor gestione connessione per più file flat** per selezionare un gruppo di file con lo stesso formato di dati e per specificare il loro formato dei dati. Una connessione per più file flat consente la connessione di un pacchetto a un gruppo di file di testo aventi lo stesso formato.  
  
 Per ulteriori informazioni sulla gestione connessione per più file flat, vedere [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Nome gestione connessione**  
 Consente di specificare un nome univoco per la connessione per più file flat nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di aggiungere una descrizione per la connessione. È consigliabile includere nella descrizione informazioni sugli scopi della connessione, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **Nomi file**  
 Consente di digitare il percorso e i nomi dei file da utilizzare nella connessione per più flat file. È possibile specificare più file usando caratteri jolly, ad esempio "C:\\\*.txt", oppure il carattere barra verticale (|) per separare più nomi di file. Tutti i file devono avere lo stesso formato data.  
  
 **Sfoglia**  
 Consente di cercare i nomi dei file da utilizzare nella connessione per più file flat. È possibile selezionare più file. Tutti i file devono avere lo stesso formato data.  
  
 **Impostazioni locali**  
 Consente di specificare la località per specificare informazioni relative all'ordinamento e alla conversione di data e ora.  
  
 **Unicode**  
 Indica se utilizzare il formato Unicode. L'utilizzo di Unicode impedisce di specificare una tabella codici.  
  
 **Tabella codici**  
 Consente di specificare la tabella codici per il testo non Unicode.  
  
 **Formato**  
 Consente di indicare se utilizzare la formattazione non allineata a destra, a larghezza fissa o delimitata. Tutti i file devono avere lo stesso formato data.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Delimitato|Le colonne sono separate dai delimitatori specificati nella pagina **Colonne** .|  
|A larghezza fissa|Le colonne hanno una larghezza fissa, specificata trascinando le linee dei marcatori nella pagina **Colonne** .|  
|Non allineato a destra|I file non allineati a destra sono file in cui ogni colonna ha una larghezza fissa, ad eccezione dell'ultima colonna, delimitata dal delimitatore di riga, che viene specificato nella pagina **Colonne** .|  
  
 **Qualificatore di testo**  
 Consente di specificare il qualificatore di testo da utilizzare. È possibile, ad esempio, racchiudere il testo tra virgolette.  
  
 **Delimitatore riga di intestazione**  
 Consente di selezionare il delimitatore per la riga di intestazione nell'elenco dei delimitatori disponibili oppure di immettere il testo per il delimitatore.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**{CR}{LF}**|La riga di intestazione è delimitata dalla combinazione di caratteri ritorno a capo/avanzamento riga.|  
|**{CR}**|La riga di intestazione è delimitata da un carattere di ritorno a capo.|  
|**{LF}**|La riga di intestazione è delimitata da un carattere di avanzamento riga.|  
|**Punto e virgola {;}**|La riga di intestazione è delimitata da un carattere punto e virgola.|  
|**Due punti {:}**|La riga di intestazione è delimitata da un carattere due punti.|  
|**Virgola {,}**|La riga di intestazione è delimitata da una virgola.|  
|**Tabulazione {t}**|La riga di intestazione è delimitata da un carattere di tabulazione.|  
|**Barra verticale {&#124;}**|La riga di intestazione è delimitata da una barra verticale.|  
  
 **Righe di intestazione da ignorare**  
 Consente di specificare il numero di righe di intestazione da ignorare, se presenti.  
  
 **Nomi di colonne nella prima riga di dati**  
 Consente di indicare se prevedere o fornire nomi di colonne nella prima riga di dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
