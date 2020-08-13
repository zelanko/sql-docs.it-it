---
title: Proprietà Alias (scheda Alias)
description: Usare la scheda Alias della finestra di dialogo Proprietà per configurare un alias e usare così un nome alternativo per la connessione a un'istanza di SQL Server.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 098da595a57c82e4d0ff68713880f38fe6acb6d2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902193"
---
# <a name="ltaliasgt-properties-alias-tab"></a>Proprietà &lt;Alias&gt; (scheda Alias)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

Un alias rappresenta un nome alternativo che può essere utilizzato per stabilire una connessione. L'alias incapsula gli elementi necessari di una stringa di connessione e li espone con un nome scelto dall'utente. Usare la pagina **Alias** nella finestra di dialogo **Proprietà \<**Alias name**>** per visualizzare o specificare gli elementi della stringa di connessione di un alias.

## <a name="options"></a>Opzioni

**Nome alias**

Nome o alias che si desidera utilizzare per fare riferimento alla connessione.  

**Nome pipe** / **Numero porta**  

Elementi aggiuntivi della stringa di connessione. Il nome di questa casella varia a seconda del protocollo selezionato. Per esempi, vedere gli argomenti elencati di seguito.  

**Protocollo**

Protocollo utilizzato per la connessione.

**Server**

Nome dell'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si esegue la connessione.  

## <a name="see-also"></a>Vedere anche

- [Creazione di una stringa di connessione valida mediante il protocollo di memoria condivisa](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [Creazione di una stringa di connessione valida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [Creazione di una stringa di connessione valida tramite named pipe](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)