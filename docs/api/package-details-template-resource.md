---
title: Шаблон URL-адреса сведений о пакете, API NuGet
description: Шаблон URL сведений о пакете позволяет клиентам отображать в пользовательском интерфейсе веб-ссылку на дополнительные сведения о пакете.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488166"
---
# <a name="package-details-url-template"></a>Шаблон URL-адреса сведений о пакете

Клиент может создать URL-адрес, который будет использоваться пользователем для просмотра дополнительных сведений о пакете в веб-браузере. Это полезно, когда источник пакета хочет показать дополнительные сведения о пакете, который может не попадать в область действия клиентского приложения NuGet.

Ресурс, используемый для создания этого URL-адреса `PackageDetailsUriTemplate` , — это ресурс, найденный в [индексе службы](service-index.md).

## <a name="versioning"></a>Управление версиями

Используются следующие `@type` значения:

Значение@type                     | Примечания
------------------------------- | -----
Паккажедетаилсуритемплате/5.1.0 | Первоначальный выпуск

## <a name="url-template"></a>Шаблон URL-адреса

URL-адрес следующего API — это значение `@id` свойства, связанное с одним из вышеупомянутых значений ресурсов. `@type`

## <a name="http-methods"></a>Методы HTTP

Хотя клиент не предназначен для выполнения запросов к URL-адресу сведений о пакете от имени пользователя, веб-страница должна поддерживать `GET` метод, позволяющий легко открывать URL-адреса, открытые в браузере.

## <a name="construct-the-url"></a>Создание URL-адреса

При наличии известного идентификатора и версии пакета реализация клиента может создать URL-адрес, используемый для доступа к веб-интерфейсу. Реализация клиента должна отображать этот сконструированный URL-адрес (или щелкнув ссылку) для пользователя, который позволяет ему открыть веб-браузер с URL-адресом и получить дополнительные сведения о пакете. Содержимое страницы сведений о пакете определяется реализацией сервера.

URL-адрес должен быть абсолютным URL-адресом, а схема (протокол) должна быть HTTPS.

Значение `@id` в индексе службы является строкой URL-адреса, содержащей любой из следующих маркеров заполнителя:

### <a name="url-placeholders"></a>Заполнители URL-адресов

name        | Тип    | Обязательно | Примечания
----------- | ------- | -------- | -----
`{id}`      | string  | Нет       | Идентификатор пакета для получения сведений
`{version}` | string  | Нет       | Версия пакета для получения сведений

Сервер должен принимать `{id}` значения и `{version}` с любым регистром. Кроме того, сервер не должен быть чувствительным к [нормализации](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers)версии. Другими словами, сервер должен принять также и ненормализованные версии.

Например, шаблон сведений о пакете NuGet. org выглядит следующим образом:

    https://www.nuget.org/packages/{id}/{version}

Если клиентская реализация должна отобразить ссылку на сведения о пакете для NuGet. Управление версиями 4.3.0, он создаст следующий URL-адрес и предоставит его пользователю:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
