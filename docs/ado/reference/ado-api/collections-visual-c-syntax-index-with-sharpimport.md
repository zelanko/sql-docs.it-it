---
title: 'Raccolte (Visual C++ indice della sintassi con #import) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'syntax indexes [ADO], ADO for Visual C++ syntax with #import'
- 'collections [ADO], ADO for Visual C++ syntax with #import'
- 'ADO for Visual C++ syntax with #import [ADO]'
- '#import [ADO]'
ms.assetid: 36fbca8e-1884-44b5-806b-d15e30f42fe6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a45203c50555168d2cd163c8b97406b8377694
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919892"
---
# <a name="collections-visual-c-syntax-index-with-import"></a>Raccolte (Visual C++ indice della sintassi con #import)
È utile tenere presente che le raccolte ereditano determinati metodi e proprietà comuni.  
  
 Tutte le raccolte ereditano la proprietà **count** e il metodo **Refresh** e tutte le raccolte aggiungono la proprietà **Item** . La raccolta **Errors** aggiunge il metodo **Clear** . La **raccolta Parameters** eredita i metodi **Append** ed **Delete** , mentre la raccolta **Fields** aggiunge i metodi **Append**, **Delete**e **Update** .  
  
## <a name="properties-collection"></a>Raccolta delle proprietà  
  
### <a name="methods"></a>Metodi  
  
```  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="errors-collection"></a>Raccolta di errori  
  
### <a name="methods"></a>Metodi  
  
```  
HRESULT Clear( );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="parameters-collection"></a>Raccolta Parameters  
  
### <a name="methods"></a>Metodi  
  
```  
HRESULT Append( IDispatch * Object );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="fields-collection"></a>Raccolta Fields  
  
### <a name="methods"></a>Metodi  
  
```  
HRESULT Append( _bstr_t Name, enum DataTypeEnum Type, long DefinedSize, enum FieldAttributeEnum Attrib, const _variant_t & FieldValue = vtMissing );  
HRESULT Delete( const _variant_t & Index );  
HRESULT Refresh( );  
HRESULT Update( );  
```  
  
### <a name="properties"></a>Proprietà  
  
```  
long GetCount( ); __declspec(property(get=GetCount)) long Count;  
PropertyPtr GetItem( const _variant_t & Index ); __declspec(property(get=GetItem)) PropertyPtr Item[];  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta Errors (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Raccolta Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
