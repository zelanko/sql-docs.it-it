---
title: Creare un file con estensione jar di Java da file di classe
description: Informazioni su come creare un file con estensione jar di Java da file di classe
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e5a53eb4b8da04a799461dcb1e0cb32feff2fe6f
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658861"
---
# <a name="create-a-java-jar-file-from-class-files"></a>Creare un file con estensione jar di Java da file di classe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Informazioni su come creare un pacchetto per assemblare i file di classe in un file con estensione jar quando si usano le [estensioni del linguaggio di SQL Server](../language-extensions-overview.md) per eseguire codice Java. Creare un pacchetto dei file è la procedura consigliata.

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

+ [Come chiamare il runtime Java nelle estensioni del linguaggio di SQL Server](../how-to/call-java-from-sql.md)