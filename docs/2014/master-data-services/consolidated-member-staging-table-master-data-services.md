---
title: Tabella di gestione temporanea di membri consolidati (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- database [Master Data Services], attributes staging table
- attributes staging table [Master Data Services]
ms.assetid: 070681ed-be99-49ae-93bd-6402f2134ace
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: bcb553e6762580c20aa3fc126f2f1576d1d5ff68
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582485"
---
# <a name="consolidated-member-staging-table-master-data-services"></a>Tabella di gestione temporanea di membri consolidati (Master Data Services)
  Usare la tabella di staging dei membri consolidati (stg.name_Consolidated) nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per creare, aggiornare, disattivare ed eliminare i membri consolidati. Inoltre, è possibile utilizzarla per aggiornare i valori degli attributi per i membri consolidati.  
  
##  <a name="TableColumns"></a> Colonne della tabella  
 Nella seguente tabella viene illustrato il motivo per cui viene utilizzato ogni campo della tabella di staging Consolidato.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|**ID**|Un identificatore assegnato automaticamente. Non immettere un valore in questo campo. Se il batch non è stato elaborato, questo campo è vuoto.|  
|**ImportType**<br /><br /> Obbligatorio|Determina l'azione da effettuare quando i dati in gestione temporanea corrispondono a dati già esistenti nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> **0**: Crea nuovi membri. Sostituire i dati MDS esistenti con i dati in gestione temporanea, ma solo se i dati in gestione temporanea non sono NULL. I valori NULL vengono ignorati. Per modificare un valore di attributo in NULL, usare **~NULL~**.<br /><br /> **1**: Crea solo nuovi membri. Qualsiasi aggiornamento ai dati MDS esistenti avrà esito negativo.<br /><br /> **2**: Crea nuovi membri. Sostituire i dati MDS esistenti con i dati in gestione temporanea. Se si importano valori NULL, i valori MDS esistenti verranno sovrascritti.<br /><br /> **3**: Disattiva il membro, in base al valore di Code. Tutti gli attributi, le appartenenze a gerarchie e raccolte e le transazioni vengono gestiti, ma non sono più disponibili nell'interfaccia utente. Se il membro viene utilizzato come valore di attributo basato su dominio di un altro membro, la disattivazione ha esito negativo.<br /><br /> **4**: Elimina definitivamente il membro, in base al valore di Code. Tutti gli attributi, le appartenenze a gerarchie e raccolte e le transazioni vengono eliminati in modo definitivo. Se il membro viene utilizzato come valore di attributo basato su dominio di un altro membro, l'eliminazione ha esito negativo.|  
|**ImportStatus_ID**<br /><br /> Obbligatorio|Lo stato del processo di importazione. I valori possibili sono:<br /><br /> **0**, specificato per indicare che il record è pronto per la gestione temporanea.<br /><br /> **1**, assegnato automaticamente indica che il processo di gestione temporanea del record ha avuto esito positivo.<br /><br /> **2**, assegnato automaticamente e indica che il processo di gestione temporanea del record non è riuscito.|  
|**Batch_ID**<br /><br /> Richiesto solo dal servizio Web|Un identificatore assegnato automaticamente che raggruppa i record per la gestione temporanea. A tutti i membri nel batch viene assegnato questo identificatore, visualizzato nella colonna [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ID **dell'interfaccia utente di** .<br /><br /> Se il batch non è stato elaborato, questo campo è vuoto.|  
|**BatchTag**<br /><br /> Richiesto, salvo che dal servizio Web|Un nome univoco per il batch, composto da un massimo di 50 caratteri.|  
|**HierarchyName**<br /><br /> Obbligatorio|Il nome della gerarchia esplicita. Ogni membro consolidato può appartenere solo ad un'unica gerarchia.|  
|**ErrorCode**|Visualizza un codice di errore. Per tutti i record con **ImportStatus_ID** di **2**, vedere [Errori del processo di gestione temporanea &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md).|  
|**Code**<br /><br /> Richiesto, tranne quando i codici vengono generati automaticamente per **ImportType1** o **2**. Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](../../2014/master-data-services/automatic-code-creation-master-data-services.md)|Un codice univoco per il membro.|  
|**Name**<br /><br /> Facoltativo|Nome per il membro.|  
|**NewCode**|Utilizzare solo se si sta modificando il codice membro.|  
|\<Nome attributo >|Esiste una colonna per ogni attributo dell'entità. Utilizzarlo con **ImportType** uguale a **0** o a **2**. Per gli attributi in formato libero specificare il nuovo testo o valore stringa per l'attributo. Per gli attributi basati su dominio specificare il codice del membro che sarà utilizzato come attributo. Per gli attributi di collegamento, l'URL deve iniziare con **http://**.<br /><br /> Nota: Non è possibile utilizzare la gestione temporanea per gli attributi di file.|  
  
## <a name="see-also"></a>Vedere anche  
 [Caricare o aggiornare membri in Master Data Services tramite il processo di gestione temporanea](add-update-and-delete-data-master-data-services.md)   
 [Spostare membri di gerarchie esplicite tramite il processo di gestione temporanea &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Importazione di dati &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Visualizzare gli errori che si verificano durante il processo di gestione temporanea &#40;Master Data Services&#41;](view-errors-that-occur-during-staging-master-data-services.md)   
 [Errori del processo di gestione temporanea &#40;Master Data Services&#41;](staging-process-errors-master-data-services.md)  
  
  
