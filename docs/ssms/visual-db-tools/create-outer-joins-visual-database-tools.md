---
title: Creare outer join
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- outer joins
- joins [SQL Server], outer
ms.assetid: 18de47b1-f936-427d-b852-fe6d20334f71
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 5c1a8b952d0723c4fd1c54ab2b841ed818017c9f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254311"
---
# <a name="create-outer-joins-visual-database-tools"></a>Creazione di join esterni (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Per impostazione predefinita, in [Progettazione query e Progettazione viste](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) viene creato un inner join tra le tabelle. Le righe prive di corrispondenza nell'altra tabella vengono eliminate. Gli outer join restituiscono invece tutte le righe di almeno una delle tabelle o viste specificate nella clausola FROM, a condizione che tali righe soddisfino una delle condizioni di ricerca della clausola WHERE o HAVING. Se si desidera includere nel set di risultati le righe di dati che non hanno una corrispondenza nella tabella in join, sarà possibile creare un outer join.  
  
Durante la creazione di un outer join, l'ordine di inserimento delle tabelle nell'istruzione SQL (riflesso nel riquadro SQL) è significativo. La prima tabella aggiunta diventa la tabella di sinistra ("left") e la seconda diventa la tabella di destra ("right"). Non è invece significativo l'ordine effettivo in cui le tabelle sono visualizzate nel [riquadro Diagramma](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) . Quando si specifica un left outer join o un right outer join, si fa riferimento alla sequenza di inserimento delle tabelle nella query o all'ordine in cui vengono visualizzate nell'istruzione SQL nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md).  
  
### <a name="to-create-an-outer-join"></a>Per creare un outer join  
  
1.  Creare un join, automaticamente o manualmente. Per informazioni dettagliate, vedere [Unione di tabelle in modo automatico &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md) o [Unione di tabelle in modo manuale &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-manually-visual-database-tools.md).  
  
2.  Selezionare la linea di join nel riquadro Diagramma e scegliere **Seleziona tutte le righe da**  dal menu **Progettazione query<tablename>** . Il comando da scegliere è quello relativo alla tabella contenente le righe supplementari da inserire.  
  
    -   Scegliere la prima tabella per creare un left outer join.  
  
    -   Scegliere la seconda tabella per creare un right outer join.  
  
    -   Scegliere entrambe le tabelle per creare un full outer join.  
  
Quando si specifica un outer join, la linea di join verrà modificata automaticamente a indicare l'outer join.  
  
Inoltre, l'istruzione SQL nel riquadro SQL verrà modificata in modo da riflettere la modifica del tipo di join, come mostrato nella seguente istruzione:  
  
```  
SELECT employee.job_id, employee.emp_id,  
   employee.fname, employee.minit, jobs.job_desc  
FROM employee LEFT OUTER JOIN jobs ON   
    employee.job_id = jobs.job_id  
```  
  
Dato che l'outer join include le righe prive di corrispondenza, è possibile utilizzarlo per trovare le righe che violano vincoli di chiave esterna. Per eseguire questa operazione, è possibile creare un outer join, quindi aggiungere una condizione di ricerca che consenta di trovare le righe in cui la colonna chiave primaria della tabella a destra sia di tipo Null. L'outer join illustrato di seguito consente ad esempio di trovare nella tabella `employee` le righe a cui non corrisponde alcuna riga nella tabella `jobs` :  
  
```  
SELECT employee.emp_id, employee.job_id  
FROM employee LEFT OUTER JOIN jobs   
   ON employee.job_id = jobs.job_id  
WHERE (jobs.job_id IS NULL)  
```  
  
## <a name="see-also"></a>Vedere anche  
[Eseguire query con join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
[Finestra di dialogo Join &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md)  
  
