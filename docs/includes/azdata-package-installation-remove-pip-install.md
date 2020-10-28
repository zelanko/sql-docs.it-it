---
author: MikeRayMSFT
ms.prod: sql
ms.topic: include
ms.date: 01/07/2020
ms.author: mikeray
ms.openlocfilehash: 0c15fb58bb076724402ab72f81e58ce46c8b7b1e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257406"
---
### <a name="pythonpip-installation"></a>Installazione di Python/PIP

È possibile installare [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] in Linux con yum, Apt o zypper oppure in MacOS con i gestori di pacchetti di installazione Homebrew. Prima che questi strumenti di gestione pacchetti fossero disponibili, l'installazione richiedeva Python e pip.

>[!IMPORTANT]
>Prima di procedere è necessario rimuovere tutte le installazioni di `azdata` nel sistema globale Python. I nuovi programmi di installazione o i pacchetti nativi aggiungono `azdata` al percorso e non è possibile sapere quale ha la precedenza.
Se si dispone di un `azdata` esistente installato nel sistema globale Python, rimuoverlo prima di procedere.

Per visualizzare l'installazione corrente, eseguire il comando seguente:

```bash
$ pip list --format columns
```

Se `azdata` viene installato da pip restituisce il pacchetto e la versione. Ad esempio:

```
 Package             Version
------------------- ----------
azdata-cli          15.0.X
azdata-cli-app      15.0.X
azdata-cli-cluster  15.0.X
azdata-cli-core     15.0.X
azdata-cli-hdfs     15.0.X
azdata-cli-notebook 15.0.X
azdata-cli-profile  15.0.X
azdata-cli-spark    15.0.X
azdata-cli-sql      15.0.X
```

Nell'esempio seguente viene rimossa un'installazione pip di `azdata`.

```bash
$ pip freeze | grep azdata-* | xargs pip uninstall -y
```

Dopo aver verificato che siano state rimosse tutte le installazioni di `azdata` installate con pip, procedere con l'installazione desiderata.