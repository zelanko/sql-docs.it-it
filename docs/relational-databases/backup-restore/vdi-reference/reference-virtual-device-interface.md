---
title: Informazioni di riferimento sull'interfaccia dispositivo virtuale
titlesuffix: SQL Server VDI reference
description: Questo articolo offre una panoramica delle informazioni di riferimento sull'interfaccia dispositivo virtuale per il backup di SQL Server.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 67bb50962ac085ba9d2397bcddd5597b87d0cce8
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128888"
---
# <a name="virtual-device-interface-vdi-reference"></a>Informazioni di riferimento sull'interfaccia dispositivo virtuale (VDI, Virtual Device Interface)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Questa sezione include le specifiche per le API di SQL Server destinate all'uso da parte di fornitori di software di backup di terze parti.

## <a name="overview"></a>Panoramica

L'interfaccia dispositivo virtuale (VDI) offre la massima velocità effettiva di backup online con una riduzione minima delle prestazioni per il carico di lavoro delle transazioni, nonché i tempi di ripristino più rapidi possibili. Consente ai fornitori di terze parti di ottenere le stesse caratteristiche di prestazioni del backup/ripristino nativo di SQL Server e rende disponibile la gamma completa di funzionalità di backup/ripristino. L'interfaccia VDI è stata introdotta in SQL Server 7.0 ed è supportata e migliorata nelle versioni successive.

VDI supporta due tipi principali di tecnologie di backup:

- Backup online convenzionali in cui l'intero contenuto del set di backup viene letto e trasferito nei supporti di backup.

- Backup snapshot tramite la tecnologia sottostante split-mirror o copy-on-write.

I backup online convenzionali eseguiti tramite VDI possono sfruttare la gamma completa di funzionalità di backup e ripristino in SQL Server. I backup snapshot sono limitati solo ai backup completi di database e file/filegroup. Tuttavia, è possibile eseguire il roll forward dei backup snapshot con backup convenzionali differenziali del database, differenziali dei file e del log delle transazioni.

## <a name="next-steps"></a>Passaggi successivi

Vedere la documentazione di riferimento per l'interfaccia VDI in questa sezione.

Scaricare la specifica completa e i file di origine di supporto:

[SQL Server 2005 Virtual Backup Device Interface (VDI) Specification](https://www.microsoft.com/download/details.aspx?id=17282) (Specifica di SQL Server 2005 Virtual Backup Device Interface - VDI)