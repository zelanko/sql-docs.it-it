---
title: STContains (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STContains method (geography)
ms.assetid: b10e8f0a-2926-449a-82ea-be42543420ca
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 6aa5b37955db2aace7785f7a39b768807e7b0e3d
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65937144"
---
# <a name="stcontains--geography-data-type"></a>STContains (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Specifica se l'istanza **geography** chiamante contiene a livello spaziale l'istanza **geography** passata al metodo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
.STContains ( other_geography )  
```  
  
## <a name="arguments"></a>Argomenti  
 *other_geography*  
 Altra istanza **geography** da confrontare con l'istanza sulla quale viene chiamato `STContains()`.  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **bit**  
  
 Tipo CLR restituito: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 Restituisce 1 se l'istanza **geography** chiamante contiene a livello spaziale l'istanza **geography** passata al metodo; in caso contrario, restituisce 0. Restituisce **null** se gli identificatori SRID delle due istanze **geography** non sono uguali.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene utilizzato `STContains()` per verificare se per due istanze `geography` la prima contiene completamente la seconda.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::Parse('CURVEPOLYGON (COMPOUNDCURVE (CIRCULARSTRING (-122.200928 47.454094, -122.810669 47.00648, -122.942505 46.687131, -121.14624 45.786679, -119.119263 46.183634), (-119.119263 46.183634, -119.273071 47.107523, -120.640869 47.569114, -122.200928 47.454094)))');  
SET @h = geography::Parse('POINT(-121.703796 46.893985)');  
```  
  
 `SELECT @g.STContains(@h);`  
  
  
