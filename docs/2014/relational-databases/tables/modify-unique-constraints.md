---
title: Modificare vincoli UNIQUE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8bb3daf170e25abc9b346aeaedb4b835cae2dfdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68809925"
---
# <a name="modify-unique-constraints"></a>Modificare vincoli univoci
  È possibile modificare un vincolo UNIQUE in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per modificare un vincolo UNIQUE usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Per modificare un vincolo UNIQUE  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse sulla tabella che contiene il vincolo UNIQUE e selezionare **Progetta**.  
  
2.  Scegliere **Indici/chiavi...** nel menu **Progettazione tabelle**.  
  
3.  Nella finestra di dialogo **Indici/chiavi** selezionare dall'elenco **Indice o chiave primari/univoci selezionati**il vincolo che si desidera modificare.  
  
4.  Completare un'operazione dalla tabella seguente:  
  
    |A|seguire le operazioni di seguito riportate|  
    |--------|------------------------|  
    |Cambiare le colonne a cui è associato il vincolo|1) In **(Generale)** all'interno della griglia fare clic su **Colonne** e quindi sui puntini di sospensione **(...)** a destra della proprietà.<br /><br /> 2) Nella finestra di dialogo **Colonne indice** specificare la nuova colonna o l'ordinamento o entrambi per l'indice.|  
    |Rinominare il vincolo|In **Identità**all'interno della griglia, digitare un nuovo nome nella casella di testo **Nome** . Scegliere un nome che non sia ancora presente nell'elenco **Indice o chiave primari/univoci selezionati** .|  
    |Impostare l'opzione cluster|Nella griglia sotto **Progettazione tabelle** selezionare **Crea come CLUSTERED** e nell'elenco a discesa scegliere Sì per creare un indice cluster e No per crearne uno non cluster. Per ogni tabella è possibile creare un solo indice cluster. Se esiste già un indice cluster in questa tabella, deselezionare questa opzione sull'indice originale.|  
    |Definire un fattore di riempimento|In **Progettazione tabelle**all'interno della griglia espandere la categoria **Specifica riempimento** e digitare un numero intero compreso tra 0 e 100 nella casella **Riempimento** .|  
  
5.  Scegliere **Salva** **nome tabella** dal menu _File_.  
  
##  <a name="TsqlProcedure"></a>**Per modificare un vincolo UNIQUE**  
  
 Per modificare un vincolo UNIQUE utilizzando Transact-SQL, è innanzitutto necessario eliminare il vincolo UNIQUE esistente e quindi ricrearlo con la nuova definizione. Per ulteriori informazioni, vedere [Delete Unique Constraints](delete-unique-constraints.md) e [Create Unique Constraints](create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
