---
title: Esempio che illustra l'uso del provider Azure Key Vault con Always Encrypted abilitato con enclave sicure | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: a4ba44733d2a14323f128f1ab105e79169b90cce
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75250939"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>Esempio che illustra l'uso del provider Azure Key Vault con Always Encrypted abilitato con enclave sicure

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

Questo esempio illustra l'uso del provider Azure Key Vault per l'accesso alle colonne crittografate.

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

## <a name="see-also"></a>Vedere anche

- [Esempio che illustra l'uso del provider Azure Key Vault con Always Encrypted](azure-key-vault-example.md)
- [Esercitazione: Sviluppare un'applicazione .NET usando Always Encrypted con enclave sicure](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Uso di Always Encrypted con il provider di dati Microsoft .NET per SQL Server](sqlclient-support-always-encrypted.md)
