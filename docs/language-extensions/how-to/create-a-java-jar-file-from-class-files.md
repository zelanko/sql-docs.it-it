---
title: Creare un file con estensione jar di Java da file di classe
titleSuffix: SQL Server Language Extensions
description: Informazioni su come creare un file con estensione jar di Java da file di classe
author: dphansen
ms.author: davidph
ms.date: 07/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4cec311a28f9d5119b5a0aeb696597e8b34ba25a
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/30/2019
ms.locfileid: "73588775"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Creare un file con estensione jar di Java da file di classe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Se si usano le [estensioni del linguaggio di SQL Server](../language-extensions-overview.md) e si esegue un codice Java, è consigliabile assemblare i file di classe in un file con estensione jar.

## <a name="create-a-jar-file"></a>Creare un file con estensione jar

Per creare un file con estensione jar da file di classe, passare alla cartella contenente il file di classe ed eseguire il comando seguente:

```cmd
jar -cf <MyJar.jar> *.class
```

Verificare che il percorso di `jar.exe` sia incluso nella variabile di sistema Path. In alternativa, specificare il percorso completo del file con estensione jar, disponibile nella directory `/bin` della cartella JDK. Esempio:

```cmd
C:\Users\MyUser\Desktop\jdk1.8.0_201\bin\jar -cf <MyJar.jar> *.class
```

## <a name="next-steps"></a>Passaggi successivi

+ [Come chiamare Java in SQL Server](../how-to/call-java-from-sql.md)