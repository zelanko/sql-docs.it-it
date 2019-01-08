---
title: Salva copia del pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1c9018dcf8ae02d939f7ba3bc29d46231ef39d1f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545553"
---
# <a name="save-copy-of-package"></a>Salva copia del pacchetto
  Usare la finestra di dialogo **Salva copia del pacchetto**, disponibile in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], per salvare una copia di un pacchetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] da [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] in un percorso diverso ed eventualmente modificarne il livello di protezione.  
  
## <a name="options"></a>Opzioni  
 **Posizione pacchetto**  
 Consente di selezionare il tipo di percorso di archiviazione in cui salvare la copia del pacchetto. Sono disponibili le opzioni seguenti:  
  
 **SQL Server**  
  
 **File system**  
  
 **Archivio pacchetti SSIS**  
  
 **Server**  
 Consente di digitare il nome del server o di selezionarlo nell'elenco. Questa opzione è disponibile solo se il percorso di archiviazione è **SQL Server** o **Archivio pacchetti SSIS**.  
  
 **Autenticazione**  
 Consente di selezionare l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Questa opzione è disponibile solo se è stato selezionato il percorso di archiviazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Se possibile, utilizzare l'autenticazione di Windows.  
  
 **Tipo di autenticazione**  
 Consente di selezionare un tipo di autenticazione.  
  
 **Nome utente**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare un nome utente.  
  
 **Password**  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare una password.  
  
 **Percorso pacchetto**  
 Digitare il percorso del pacchetto oppure fare clic su Sfoglia **(...)**  pulsante e individuare la cartella in cui archiviare il pacchetto.  
  
 **Livello di protezione**  
 Fare clic su Sfoglia **(...)**  pulsante e aggiornare il livello di protezione nel **livello di protezione pacchetto** nella finestra di dialogo. Per altre informazioni, vedere [Finestra di dialogo Livello di protezione pacchetto e Livello di protezione del progetto](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'interfaccia utente della finestra di dialogo Importa pacchetto](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Riferimento all'interfaccia utente della finestra di dialogo Esporta pacchetto](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Salvataggio di pacchetti](save-packages.md)   
 [Importare ed esportare pacchetti &#40;servizio SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
