---
description: Proprietà ParentCatalog (ADOX)
title: Proprietà ParentCatalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: rothja
ms.author: jroth
ms.openlocfilehash: 07e4cdabe09b2bc4af8e849ef367df65c23711ca
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983772"
---
# <a name="parentcatalog-property-adox"></a>Proprietà ParentCatalog (ADOX)
Specifica il catalogo padre di una tabella, di un utente o di un oggetto colonna per fornire l'accesso alle proprietà specifiche del provider.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta e restituisce un oggetto [Catalogo](./catalog-object-adox.md) . L'impostazione di **ParentCatalog** su un **Catalogo** aperto consente l'accesso alle proprietà specifiche del provider prima di accodare una tabella o una colonna a una raccolta di **cataloghi** .  
  
## <a name="remarks"></a>Osservazioni  
 Alcuni provider di dati consentono la scrittura di valori di proprietà specifici del provider solo in fase di creazione, ovvero quando una tabella o una colonna viene aggiunta alla relativa raccolta di **cataloghi** . Per accedere a queste proprietà prima di accodare questi oggetti a un **Catalogo**, specificare prima il **Catalogo** nella proprietà **ParentCatalog** .  
  
 Si verifica un errore quando la tabella o la colonna viene aggiunta a un **Catalogo** diverso da quello di **ParentCatalog**.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Column (ADOX)](./column-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto Table (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [Oggetto User (ADOX)](./user-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio della proprietà ParentCatalog (VB)](./parentcatalog-property-example-vb.md)