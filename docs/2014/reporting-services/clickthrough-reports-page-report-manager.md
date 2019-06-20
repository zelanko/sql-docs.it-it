---
title: Report click-through pagina (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.drilthroughreports.f1
ms.assetid: e96cdeba-452b-45a8-9bcf-b75d76261e31
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d996463baaed3095b6866fa2da88ed811745878d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109803"
---
# <a name="clickthrough-reports-page-report-manager"></a>Pagina Report click-through (Gestione report)
  Un report click-through consente di visualizzare una tabella di dati correlati quando si fa clic sui dati interattivi inclusi nel report. Questi report vengono generati dal server di report in base alle informazioni incluse nel modello utilizzato per creare il report. Se non si desidera utilizzare i report click-through generati dal server di report, è possibile creare report personalizzati da pubblicare in un server di report e di cui eseguire il mapping a punti dati interattivi definiti nel modello. I report personalizzati devono essere creati in Generatore report dallo stesso modello, quindi pubblicati nel server di report. Per eseguire il mapping dei report personalizzati agli elementi nel modello, utilizzare la pagina Report click-through in Gestione report.  
  
 La pagina Report click-through consente di eseguire il mapping tra report di Generatore report pubblicati e predefiniti ed entità, cartelle ed elementi specifici di un modello. Quando si esegue il mapping tra un report e un elemento di un modello, gli utenti che si spostano su tale elemento visualizzano il report personalizzato anziché un report temporaneo generato dal server di report.  
  
 Se si distribuiscono report personalizzati, è necessario includere sia una versione a istanza singola che una versione multi-istanza del report. Il percorso dei dati in base al quale un utente si sposta su un'entità specifica determina se, in fase di esecuzione, a tale utente verrà presentato un report a istanza singola o multi-istanza. Non è sempre possibile conoscere in anticipo se una determinata versione del report non sarà necessaria.  
  
 I report personalizzati di cui si esegue il mapping a entità sono protetti tramite la gerarchia di cartelle del server di report. Se si esegue il mapping tra un elemento di un modello e un report e l'utente che si sposta su tale report non può accedervi, viene restituito un report temporaneo generato dal server di report anziché il report personalizzato previsto.  
  
 Sebbene sia possibile selezionare qualsiasi report per cui si dispone di accesso, è opportuno selezionare solo i report creati specificamente per il modello di cui si esegue la configurazione.  
  
> [!NOTE]  
>  I report click-through non sono disponibili in tutte le edizioni di [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md). Se non si è certi dell'edizione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzata nell'organizzazione, contattare l'amministratore del database.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-clickthrough-reports-page"></a>Per aprire la pagina Report click-through  
  
1.  Aprire Gestione report, individuare il modello per il quale si desidera eseguire il mapping dei report click-through a entità nel modello.  
  
2.  Passare con il puntatore del mouse sul modello, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu a discesa fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà **Generale** per il modello.  
  
4.  Selezionare la scheda **Click-through** .  
  
## <a name="options"></a>Opzioni  
 **Gerarchia degli elementi del modello**  
 Consente di visualizzare le entità, le cartelle e gli elementi inclusi nello spazio dei nomi del modello per cui è possibile specificare un report personalizzato.  
  
 **Report a istanza singola**  
 Consente di specificare il report personalizzato da utilizzare quando per la navigazione dell'utente è necessaria una visualizzazione di dati a istanza singola. Fare clic sul pulsante Sfoglia per selezionare il report che si desidera utilizzare.  
  
 **Report a più istanze**  
 Consente di specificare il report personalizzato da utilizzare quando per la navigazione dell'utente è necessaria una visualizzazione di dati a istanza multipla. Fare clic sul pulsante Sfoglia per selezionare il report che si desidera utilizzare.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di report](../../2014/reporting-services/publish-reports.md)  
  
  
