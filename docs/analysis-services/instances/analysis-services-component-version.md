---
title: Verifica della versione di build aggiornamenti cumulativi di SQL Server Analysis Services | Microsoft Docs
ms.date: 07/11/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1da8384bb51360178e1735d13f6c6b706e8b7ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659059"
---
# <a name="verify-analysis-services-cumulative-update-build-version"></a>Verificare la versione della build di aggiornamento cumulativo di Analysis Services

A partire da SQL Server 2017, il numero di versione di build di Analysis Services e il numero della versione build del motore di Database di SQL Server non corrispondono. Anche se Analysis Services e il motore di Database usare il programma di installazione stesso, i sistemi di compilazione ogni uso sono separate.

 In alcuni casi, è necessario verificare se un pacchetto di compilazione di aggiornamento cumulativo (CU) è stato applicato e i componenti di Analysis Services sono stati aggiornati. È possibile verificare tramite il confronto tra i numeri di versione build del file dei componenti di Analysis Services installata nel computer con i numeri di versione di build per una particolare CU.

## <a name="verify-component-file-version"></a>Verificare la versione del file componente

Per verificare la versione di file di componente, 

1. Passare a [versioni build di SQL Server 2017](https://support.microsoft.com/help/4047329). 
2. In **SQL Server 2017 aggiornamento cumulativo (CU) si basa**, fare clic sul **della Knowledge Base numero** per la compilazione che si desidera verificare.
3. Nel **aggiornamento cumulativo (#) per SQL Server 2017** articolo, nelle **informazioni sul pacchetto di aggiornamento cumulativo** , quindi espandere **informazioni sul file del pacchetto di aggiornamento cumulativo**.
4. Nel **SQL Server 2017 Analysis Services** tabella, controllare la versione del File per il **msmdsrv.exe** file del componente. Se è stato applicato l'aggiornamento Cumulativo, il numero di versione del file dovrebbe corrispondere al file msmdsrv.exe installato nel computer.

## <a name="see-also"></a>Vedere anche  

[Installare gli aggiornamenti di manutenzione per SQL Server](../../database-engine/install-windows/install-sql-server-servicing-updates.md)  

[Update Center di Microsoft SQL Server](https://msdn.microsoft.com/library/ff803383.aspx)
  
  
