---
title: Proprietà server (pagina Cronologia) | Microsoft Docs
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f4f3c13e6393dc935c09d54a274d2dbe357401f1
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571352"
---
# <a name="server-properties-history-page"></a>Proprietà server (pagina Cronologia)
  Usare questa pagina di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] per impostare un valore predefinito per il numero di copie di cronologia dei report da mantenere. Il valore predefinito rappresenta un'impostazione iniziale che definisce i limiti della cronologia di tutti i report. È possibile modificare queste impostazioni per singoli report.  
  
 La cronologia del report è una raccolta di snapshot del report che includono layout e dati del report al momento della creazione dello snapshot. È possibile utilizzare la cronologia del report per conservare una copia di un report in una data o un'ora specifica. È possibile creare e gestire la cronologia del report per singoli report in esecuzione in un server di report in modalità nativa o in un server di report configurato per la modalità integrata SharePoint.  
  
 Gli snapshot della cronologia del report vengono archiviati nel database del server di report. Se si conserva un numero illimitato di snapshot, controllare periodicamente la dimensione del database per verificare che non stia aumentando troppo velocemente o che non occupi troppo spazio su disco.  
  
 Per aprire questa pagina:
 1) Avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].
 2) Connettersi a un'istanza del server di report.
 3) Fare clic con il pulsante destro del mouse sul nome del server di report, quindi scegliere **Proprietà**.
 4) Fare clic su **Cronologia** per aprire la pagina.  
  
## <a name="options"></a>Opzioni  
 **Nessun limite per il numero di snapshot archiviabili nella cronologia**  
 Consente di conservare tutti gli snapshot della cronologia del report. Per mantenere ridotte le dimensioni della cronologia del report sarà necessario eliminare manualmente gli snapshot non più necessari.  
  
 **Numero massimo di copie della cronologia**  
 Consente di conservare un numero fisso di snapshot della cronologia del report. Raggiunto tale limite, le copie meno recenti vengono rimosse dalla cronologia del report per fare spazio alle copie più recenti.  
  
 Se si imposta tale limite in un momento successivo e il limite viene superato, la cronologia dei report nel server viene ridotta di conseguenza. Vengono eliminati per primi gli snapshot del report meno recenti. Se la cronologia è vuota o include un numero di snapshot inferiore al limite, vengono aggiunti nuovi snapshot del report. Quando viene raggiunto il limite, all'aggiunta di un nuovo snapshot del report viene eliminato lo snapshot meno recente.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le proprietà di un server di report &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
