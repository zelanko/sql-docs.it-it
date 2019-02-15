---
title: Finestra di dialogo Proprietà generali dell'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3c8dc6e3ca883e5d27358733df7c6f83ee8c4eab
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295559"
---
# <a name="data-source-properties-dialog-box-general"></a>Finestra di dialogo Proprietà origine dati, Generale
  Selezionare **Generale** nella finestra di dialogo **Proprietà origine dati** per visualizzare e modificare le informazioni di connessione per un'origine dati nel report.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare il nome dell'origine dati. Tale nome deve essere univoco all'interno del report. Per impostazione predefinita, all'origine dei dati viene assegnato un nome generico, ad esempio DataSource1 o DataSource2.  
  
 **Connessione incorporata**  
 Selezionare questa opzione se non si desidera utilizzare un'origine dati condivisa.  
  
 **Tipo**  
 Selezionare un'estensione per l'elaborazione dei dati. Nell'elenco vengono visualizzate tutte le estensioni registrate.  
  
 **Stringa di connessione**  
 Immettere una stringa di connessione per l'origine dati. Fare clic su **Modifica** per compilare la stringa di connessione mediante la finestra di dialogo **Proprietà connessione** . Fare clic sul pulsante **Espressioni** (*fx*) per modificare l'espressione.  
  
 **Usa riferimento a origine dati condivisa**  
 Selezionare questa opzione per definire un collegamento a un'origine dati condivisa. Selezionare un'origine dati condivisa dall'elenco a discesa. Per modificare l'origine dati selezionata, fare clic su **Modifica**. Se si seleziona **Usa riferimento a origine dei dati condivisa** , le opzioni **Tipo** e **Stringa di connessione** risulteranno disabilitate.  
  
 **Usa transazione singola durante l'elaborazione delle query**  
 Selezionare questa opzione per indicare che i set di dati che utilizzano l'origine dei dati vengono eseguiti in un'unica transazione sul database. Per includere transazioni per sottoreport che utilizzano la stessa origine dati, impostare **MergeTransactions** su **True** nella sezione **Altro** del riquadro **Proprietà** del sottoreport.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Creare un'origine dati incorporata o condivisa &#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Finestra di dialogo Proprietà origine dati, Credenziali](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
