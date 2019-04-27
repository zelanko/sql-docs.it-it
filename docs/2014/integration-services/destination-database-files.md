---
title: File di Database di destinazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4911084929f3ff69657a6d5e51c557f35929b45b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769907"
---
# <a name="destination-database-files"></a>File di database di destinazione
  Utilizzare la finestra di dialogo **File di database di destinazione** per visualizzare o modificare i percorsi e i nomi dei file di database nel server di destinazione oppure per specificare un percorso di file di rete per l'attività Trasferisci database. Per altre informazioni su questa attività, vedere [Attività Trasferisci database](control-flow/transfer-database-task.md).  
  
 Per inserire automaticamente i percorsi e i nomi dei file di database del server di origine in questa finestra di dialogo, specificare innanzitutto le proprietà **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** nella pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
## <a name="options"></a>Opzioni  
 **File di destinazione**  
 Nomi dei file di database trasferiti nel server di destinazione.  
  
 Immettere il nome del file o fare clic sul nome del file per modificarlo.  
  
 **Cartella di destinazione**  
 Cartella del server di destinazione in cui verranno trasferiti i file di database.  
  
 Immettere il percorso della cartella, fare clic su tale percorso per modificarlo oppure fare clic su Sfoglia per individuare la cartella del server di destinazione in cui trasferire i file di database.  
  
 **Condivisione file di rete**  
 Cartella di condivisione dei file di rete del server di destinazione in cui verranno trasferiti i file di database. Utilizzare **Condivisione file di rete** quando si trasferisce un database in modalità offline specificando **DatabaseOffline** per **Metodo** nella pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** .  
  
 Immettere il percorso di condivisione dei file di rete o fare clic su Sfoglia per individuarlo.  
  
 Durante il trasferimento di un database in modalità offline, prima di essere trasferiti nella posizione **Cartella di destinazione** , i file di database vengono copiati nella cartella **Condivisione file di rete** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Trasferisci database &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Trasferisci database &#40;pagina Database&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
