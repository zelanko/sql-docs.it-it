---
title: Modificare vincoli CHECK | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, modifying
- modifying constraints
- constraints [SQL Server], check
- constraints [SQL Server], modifying
ms.assetid: f22daef8-e350-40ef-8ff0-b5f87d1d9e56
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5b8a43f06a0c100725607dfc903bfd045a0d387b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067986"
---
# <a name="modify-check-constraints"></a>Modifica di vincoli CHECK
  È possibile modificare un vincolo CHECK in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)] quando si desidera modificare l'espressione del vincolo o le opzioni che lo abilitano o disabilitano al verificarsi di specifiche condizioni.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per modificare un vincolo CHECK:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-modify-a-check-constraint"></a>Per modificare un vincolo CHECK  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella che contiene il vincolo CHECK e selezionare **Progetta**.  
  
2.  Scegliere **Vincoli CHECK** nel menu **Progettazione tabelle**.  
  
3.  Nella finestra di dialogo **Vincoli CHECK** selezionare il vincolo che si desidera modificare in **Vincolo CHECK selezionato**.  
  
4.  Completare un'operazione dalla tabella seguente:  
  
    |A|seguire le operazioni di seguito riportate|  
    |--------|------------------------|  
    |Modificare l'espressione del vincolo|Digitare la nuova espressione nel campo **Espressione** .|  
    |Rinominare il vincolo|Digitare un nuovo nome nel campo **Nome** .|  
    |Applicare il vincolo a dati esistenti|Selezionare l'opzione **Verifica dati esistenti durante la creazione o l'attivazione** .|  
    |Disabilitare il vincolo in caso di aggiunta di nuovi dati alla tabella o di aggiornamento di dati esistenti nella tabella|Deselezionare l'opzione **Attiva vincolo per istruzioni INSERT e UPDATE** .|  
    |Disabilitare il vincolo quando un agente di replica accoda o aggiorna dati nella tabella.|Deselezionare l'opzione **Attiva per replica** .|  
  
    > [!NOTE]  
    >  Alcuni database dispongono di funzionalità differenti per i vincoli CHECK.  
  
5.  Fare clic su **Close**.  
  
6.  Scegliere **Salva**_nome tabella_ dal menu **File**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
 **Per modificare un vincolo CHECK**  
  
 Per modificare un vincolo `CHECK` utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)], è innanzitutto necessario eliminare il vincolo `CHECK` esistente e quindi crearlo di nuovo con la nuova definizione. Per altre informazioni, vedere [Eliminazione dei vincoli CHECK](delete-check-constraints.md) e [Creare vincoli CHECK](create-check-constraints.md).  
  
###  <a name="TsqlExample"></a>  
