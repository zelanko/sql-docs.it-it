---
title: Copiare tabelle da un diagramma di database a un altro
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- duplicating tables
ms.assetid: 155a4f09-9321-4887-a7d4-aa2ce6b51277
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 887cc2cdb2d70b0d69599d75d8534907552cb201
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254387"
---
# <a name="copy-tables-from-one-database-diagrams-to-another-visual-database-tools"></a>Copia di tabelle da un diagramma di database a un altro (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
È possibile copiare una tabella da un diagramma di database a un altro nello stesso database.  
  
Quando si esegue questa operazione, viene semplicemente aggiunto un riferimento alla tabella nel secondo diagramma. La tabella non viene duplicata nel database. Se ad esempio si copia la tabella `authors` da un diagramma di database a un altro, ogni diagramma farà riferimento alla stessa tabella `authors` nel database.  
  
### <a name="to-copy-a-table-from-another-database-diagram"></a>Per copiare una tabella da un diverso diagramma di database  
  
1.  Assicurarsi di essere connessi al database di cui si desidera copiare la tabella.  
  
2.  Aprire i diagrammi di database di origine e destinazione e, all'interno del diagramma d'origine, selezionare la tabella da copiare nel diagramma di destinazione.  
  
3.  Fare clic sul pulsante **Copia** sulla barra degli strumenti. La definizione della tabella selezionata verrà copiata negli Appunti.  
  
4.  Passare al diagramma di destinazione. Il diagramma deve essere nello stesso database del diagramma di origine.  
  
5.  Fare clic sul pulsante **Incolla** sulla barra degli strumenti. Il contenuto degli Appunti verrà inserito nella nuova posizione e rimarrà evidenziato fino a quando non si farà clic in un altro punto. Se esistono delle relazioni tra le tabelle selezionate e altre tabelle nel diagramma di destinazione, verranno tracciate automaticamente le linee delle relazioni.  
  
Le modifiche apportate alla tabella in uno dei due diagrammi verranno riportate in entrambi i diagrammi. Allo stesso modo, dopo avere salvato la tabella in uno dei due diagrammi, essa non verrà più considerata "modificata" in nessuno dei due.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzare diagrammi di database &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Aggiunta di tabelle a diagrammi &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-diagrams-visual-database-tools.md)  
  
