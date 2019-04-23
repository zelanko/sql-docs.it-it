---
title: Pagina Nuovo Report collegato (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fefb46e8-6901-4d50-a3f8-7c49ad72e7b1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f55c1fb1b90f676f3e1867c6aefdd13889c2cce
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967977"
---
# <a name="new-linked-report-page-report-manager"></a>Pagina Nuovo report collegato (Gestione report)
  La pagina Nuovo report collegato consente di creare un report collegato. Un report collegato è un report con impostazioni e proprietà proprie, ma collegato alla definizione di un altro report. I report collegati sono utili per utilizzare un report di base con alcune variazioni per gruppi o utenti specifici, ad esempio un report che restituisca dati diversi in base a un codice internazionale specificato come parametro. I report collegati vengono in genere creati da un report con parametri, se l'esigenza è quella di variare e quindi salvare valori di parametri diversi per ogni istanza del report. È comunque possibile creare un report collegato da qualsiasi report accessibile.  
  
 Un report collegato dispone di nome, descrizione, posizione, proprietà dei parametri, proprietà per l'esecuzione del report, proprietà della cronologia del report, autorizzazioni e sottoscrizioni propri. Un report collegato deve tuttavia utilizzare le stesse proprietà dell'origine dati e lo stesso layout del report di base che fornisce la definizione del report.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare le procedure riportate di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-new-linked-report-page-from-the-contents-page"></a>Per aprire la pagina Nuovo report collegato dalla pagina Contenuto  
  
1.  Aprire Gestione report e individuare un report per il quale si desidera creare un report collegato.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Nel menu di riepilogo a discesa, fare clic su **crea Report collegato**.  
  
###### <a name="to-open-the-new-linked-report-page-from-the-general-properties-page-of-a-report"></a>Per aprire la pagina Nuovo report collegato dalla pagina delle proprietà Generale di un report  
  
1.  Aprire Gestione report e individuare un report per il quale si desidera creare un report collegato.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Nella barra degli strumenti dell'elemento fare clic su **Crea report collegato**.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Specificare il nome del report collegato. Il nome deve includere almeno un carattere alfanumerico. È inoltre possibile utilizzare spazi e alcuni simboli. I caratteri ; ? : \@ & = +, $ / * \< > | "oppure / per specificare un nome.  
  
 **Descrizione**  
 Consente di digitare una descrizione del contenuto del report. Questa descrizione viene visualizzata nella pagina Contenuto per gli utenti autorizzati ad accedere al report.  
  
 **Percorso**  
 Specificare il percorso della cartella in cui è disponibile il report. Per impostazione predefinita, i report collegati vengono creati nella stessa cartella del report di base. Fare clic su **Cambia percorso** per inserire il report collegato in una cartella diversa.  
  
 **OK**  
 Fare clic su **OK** per salvare le modifiche e tornare alla pagina delle proprietà generale del report di base.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un Report collegato](reports/create-a-linked-report.md)   
 [Pagina delle proprietà Generale, Report &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
