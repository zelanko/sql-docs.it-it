---
description: Supporto per i tipi di dati di Connettore Microsoft per Oracle
title: Supporto per i tipi di dati di Connettore Microsoft per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2193c93ff55ed38ff5c629072109036306bb72c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430773"
---
# <a name="microsoft-connector-for-oracle-data-type-support"></a>Supporto per i tipi di dati di Connettore Microsoft per Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

I componenti SSIS per Oracle non supportano tutti i tipi di dati Oracle. Per le colonne con tipi di dati non supportati verrà visualizzato un avviso durante la progettazione dei pacchetti in SSDT e le colonne verranno eliminate dal mapping. Non è possibile caricare i dati in una colonna con un tipo di dati non supportato.

## <a name="data-type-mapping"></a>Mapping dei tipi di dati

Nella tabella seguente vengono illustrati i tipi di dati di Oracle Database e il mapping predefinito ai tipi di dati di SSIS. Sono anche indicati i tipi di dati Oracle non supportati.

|Tipo di dati del database Oracle|Tipo di dati SSIS|Commenti|
|:-|:-|:-|
|VARCHAR2|DT_STR||
|NVARCHAR2|DT_WSTR||
|CHAR|DT_STR||
|NUMBER|DT_R8|Il valore può essere modificato in DT_NUMERIC con una precisione e una scala specifiche. La precisione e la scala sono definite dall'utente in base alle esigenze. L'output sarà costituito dai dati della colonna sotto forma di numero con precisione e scala fisse.|
|NUMBER(P, S)| Quando la scala è 0, in base alla precisione (P) <li> DT_I1 <Li> DT_I2 <Li> DT_I4 <Li> DT_NUMBERIC(P,0)||
||DT_NUMERIC(P,S)||
|DATE|DT_DBTIMESTAMP||
|<li>timestamp <li>TIMESTAMP WITH TIME ZONE <li>INTERVAL YEAR TO MONTH <li>INTERVAL DAY TO SECOND <li>TIMESTAMP WITH LOCAL TIME ZONE|DT_STR||
|RAW|DT_BYTES||
|CLOB|DT_TEXT|I tipi di dati CLOB, NCLOB e BLOB sono supportati solo in modalità array, non in modalità di caricamento rapido.|
|NCLOB|DT_NTEXT||
|BLOB|DT_IMAGE||
|UROWID|Non Supportato||
|REF|Non Supportato||
|BFILE|Non Supportato||
|LONG|Non Supportato||
|LONG RAW|Non Supportato||
|ROWID|Non Supportato||
|Tipo definito dall'utente (tipo di oggetto, VARRAY, tabella annidata)|Non Supportato||

## <a name="next-steps"></a>Passaggi successivi

- Configurare [Gestione connessione Oracle](oracle-connection-manager.md).
- Configurare l'[origine Oracle](oracle-source.md).
- Configurare la [destinazione Oracle](oracle-destination.md).
- Per eventuali domande, visitare [TechCommunity](https://aka.ms/AA5u35j).
