---
title: Utilizzo degli oggetti di database
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f961d0aba5bb42c924f5c6174670d6e8566f662
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900064"
---
# <a name="creating-altering-and-removing-database-objects"></a>Creazione, modifica e rimozione di oggetti di database
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  Le fasi di creazione di un oggetto SMO sono le seguenti:  
  
1.  Creare un'istanza dell'oggetto.  
  
2.  Impostare le proprietà dell'oggetto.  
  
3.  Creare istanze degli oggetti figlio.  
  
4.  Impostare le proprietà degli oggetti figlio.  
  
5.  Creare l'oggetto.  

 Se vengono create istanze degli oggetti SMO in un'applicazione SMO, queste non verranno visualizzate nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] finché non viene chiamato il metodo **Crea** . Non è tuttavia necessario chiamare un metodo **Create** per ogni singolo oggetto. Se per un oggetto è presente un set di oggetti figlio, per eseguire il metodo **Create** è necessario solo l'oggetto padre. Per definire una tabella, ad esempio, è necessario che questa contenga almeno una colonna. Una colonna inoltre non può esistere senza una tabella. Esiste una relazione di interdipendenza tra la tabella e le rispettive colonne.  
  
 Il metodo <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> consente di apportare modifiche a un oggetto. Diverse modifiche a un oggetto, ad esempio l'aggiunta di oggetti figlio a una delle raccolte dell'oggetto o la modifica di un valore di proprietà, vengono eseguite in batch come modifica unica. Il metodo **Alter** riduce traffico di rete e migliora complessivamente le prestazioni.  
  
 L'istruzione **Drop** viene utilizzata per rimuovere un oggetto e tutti i rispettivi oggetti figlio interdipendenti necessari per creare inizialmente l'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti SMO](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
