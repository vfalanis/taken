---
layout: page
title: Networking
permalink: /networking/
---

Zadanie 1
----------


Plik *Api.Swift*  - w enum Endpoint brakuje obsługi 2 przypadków:

* Track(id: String) 
* Tracks(ids:[String])

uzupelnije je z następującymi wartościami :

dla Track(id: String) 
* path: "tracks/\(id)/"

dla Tracks(ids:[String])
* path: "tracks/"
* parameters: ids.encoded
* rootKeyPath: "tracks"

Zadanie 2
----------


W pliku *Api.Swift* uzupełnij funkcje

```absoluteURL(endpoint: Endpoint) -> NSURL?```

która zwraca obiekt NSURL na podstawie przekazanego argumentu *endpoint* oraz  *API.baseURL*.
 
 
Obiekt URL musi zawierać wartości z *endpoint.parameters*. 


Wykorzystaj do tego celu NSURLComponents oraz NSURLQueryItem

Zadanie 3 
----------


Uzpełnij funkcję ```request()```

Stwórz NSURL request z wykorzystaniem zaimplementowanej wcześniej metody ```absoluteURL()```.


Wykorzystaj istniejący obiekt session do stworzenia tasku użyj metody:

```session.dataTaskWithURL(<url: NSURL>, completionHandler: <(NSData?, NSURLResponse?, NSError?) -> Void>)```


Obsłuż response uwzględniając przypadki:


a) pełna serializacja danych zwróconych przez API
b) błędna serializacja danych zwróconych przez API


Do parsowania błędów zwróconych przez API użyj metody ```createNSErrorFromJson(json: JSON?) -> NSError?```
