---
title: Proprietà server (pagina Cronologia) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ce48c964ec756668aa12566c494d9ae9a1e5372
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099579"
---
# <a name="server-properties-history-page"></a>Proprietà server (pagina Cronologia)
  Utilizzare questa pagina per impostare un valore predefinito relativo al numero di copie di cronologia dei report da mantenere. Il valore predefinito rappresenta un'impostazione iniziale che definisce i limiti della cronologia di tutti i report. È possibile modificare queste impostazioni per singoli report.  
  
 La cronologia del report è una raccolta di snapshot del report che includono layout e dati del report al momento della creazione dello snapshot. È possibile utilizzare la cronologia del report per conservare una copia di un report in una data o un'ora specifica. È possibile creare e gestire la cronologia del report per singoli report in esecuzione in un server di report in modalità nativa o in un server di report configurato per la modalità integrata SharePoint.  
  
 Gli snapshot della cronologia del report vengono archiviati nel database del server di report. Se si conserva un numero illimitato di snapshot, controllare periodicamente la dimensione del database per verificare che non stia aumentando troppo velocemente o che non occupi troppo spazio su disco.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un'istanza del server di report, fare clic con il pulsante destro del mouse sul nome del server di report e scegliere **Proprietà**. Fare clic su **Cronologia** per aprire la pagina.  
  
## <a name="options"></a>Opzioni  
 **Nessun limite per il numero di snapshot archiviabili nella cronologia**  
 Consente di conservare tutti gli snapshot della cronologia del report. Per mantenere ridotte le dimensioni della cronologia del report sarà necessario eliminare manualmente gli snapshot non più necessari.  
  
 **Numero massimo di copie della cronologia**  
 Consente di conservare un numero fisso di snapshot della cronologia del report. Raggiunto tale limite, le copie meno recenti vengono rimosse dalla cronologia del report per fare spazio alle copie più recenti.  
  
 Se si imposta tale limite in un momento successivo e il limite viene superato, la cronologia dei report nel server viene ridotta di conseguenza. Vengono eliminati per primi gli snapshot del report meno recenti. Se la cronologia è vuota o include un numero di snapshot inferiore al limite, vengono aggiunti nuovi snapshot del report. Quando viene raggiunto il limite, all'aggiunta di un nuovo snapshot del report viene eliminato lo snapshot meno recente.  
  
## <a name="see-also"></a>Vedi anche  
 [Impostazione delle proprietà del server di report &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Connettersi a un server di report in Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)  
  
  
