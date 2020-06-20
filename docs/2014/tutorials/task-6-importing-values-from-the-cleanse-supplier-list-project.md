---
title: 'Attività 6: importazione di valori dal progetto cleane Supplier List | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fec0deef-a729-4ff1-b709-72d2b3f407ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: cb3e7a85254cac96b8b8541de57b494e96b8928f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061066"
---
# <a name="task-6-importing-values-from-the-cleanse-supplier-list-project"></a>Attività 6: Importazione di valori dal progetto Cleanse Supplier List
  In questa attività vengono importate le informazioni sulla qualità dei dati raccolte durante il processo di pulizia. Per altri dettagli, vedere [importazione dei valori di un progetto di pulizia in un dominio](https://msdn.microsoft.com/library/hh479581.aspx) . È inoltre possibile esportare la Knowledge base in un file DQS prima di pubblicare la Knowledge base **Suppliers** aggiornata.  
  
1.  Nella pagina principale del **client DQS**fare clic sulla **freccia a destra** accanto a **fornitori** in **Knowledge Base recenti** e quindi su **Gestione dominio**.  
  
2.  Fare clic su **Contact email** nell'elenco di domini e passare alla scheda **Domain values** nel riquadro destro.  
  
3.  Fare clic sulla **freccia giù** accanto all'icona **Importa valori** sulla barra degli strumenti e fare clic su **Importa valori progetto**.  
  
     ![Pulsante della barra degli strumenti Importa valori di progetto](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-01.jpg "Pulsante della barra degli strumenti Importa valori di progetto")  
  
4.  Nella finestra di dialogo **Importa valori progetto** selezionare il progetto **Pulisci Supplier List** , quindi fare clic su **OK**.  
  
5.  Si noti che tutti gli indirizzi di posta elettronica vengono importati insieme alle due correzioni apportate durante la pulizia interattiva. Scorrere per visualizzare le due correzioni.  
  
    |valore|Correggi in|  
    |-----------|----------------|  
    |bobby0@adventure-work.com|bobby0@adventure-works.com|  
    |tad0@adventure-work.com|tad0@adventure-works.com|  
  
6.  Ripetere il passaggio precedente dell'importazione dei valori del progetto per il dominio **Country** . si noti che è stata aggiunta una nuova voce per la correzione **dello stato United** a **Stati Uniti** (con ' s').  
  
    |valore|Correggi in|  
    |-----------|----------------|  
    |United State|Stati Uniti|  
  
7.  Per visualizzare i valori di dominio precedenti, deselezionare la casella di controllo **Mostra solo nuovo** .  
  
8.  Ripetere il passaggio precedente per importare i valori di progetto per il dominio **Supplier Name** . Per impostazione predefinita, dopo l'importazione, verranno visualizzati solo i nuovi valori. Per visualizzare tutti i valori, deselezionare la casella di controllo **Mostra solo nuovi** . La Knowledge base **Suppliers** è stata arricchita con i concetti appresi dall'attività di pulizia. Maggiore è l'attendibilità della Knowledge Base, migliori sono i risultati della pulizia.  
  
    > [!NOTE]  
    >  Non è possibile importare valori per un dominio composito.  
  
9. Fare clic sull'icona **Esporta Knowledge base** sulla barra degli strumenti e quindi fare clic su **Esporta Knowledge base**.  
  
     ![Menu Esporta Knowledge Base](../../2014/tutorials/media/et-importingvaluesfromthecslistproject-02.jpg "Menu Esporta Knowledge Base")  
  
10. Passare alla cartella tutorial, digitare **Suppliers. DQS** per il **nome del file**e fare clic su **Salva**. È possibile utilizzare questo file DQS per creare una nuova Knowledge Base basandosi su di esso.  
  
11. Fare clic su **OK** per chiudere la finestra di messaggio **Esporta Knowledge base-fornitori** .  
  
12. Fare clic su **fine** per completare l'attività.  
  
13. Fare clic su **Pubblica**.  
  
14. Fare clic su **OK** nella finestra di messaggio.  
  
## <a name="next-step"></a>passaggio successivo  
 [Lezione 3: Corrispondenza dei dati per rimuovere i duplicati dall'elenco fornitori](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)  
  
  
