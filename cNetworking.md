---
layout: page
title: Networking
permalink: /networking/
---

Zadanie 1
----------
* Api.Swift

W enum Endpoint  brakuje obsługi 2 przypadków:
* Track(id: String) 
* Tracks(ids:[String])
uzupelnije je z następującymi wartościami :

* Track(id: String) 
- path: "tracks/\(id)/"


* Tracks(ids:[String])
- path: "tracks/"
- parameters: ids.encoded
- rootKeyPath: "tracks"



uzupełnij funkcje  absoluteURL(endpoint: Endpoint) -> NSURL?
która zwraca obiekt NSURL na podstawie przekazanego argumentu endpoint oraz   API.baseURL. URL musi zawierać wartości z endpoint.parameters. Wykorzystaj do tego celu NSURLComponents oraz NSURLQueryItem

task 3 uzpełnij funkcję request()
stwórz NSURL request z wykorzystaniem zaimplementowanej wcześniej metody absoluteURL.
Wykorzystaj istniejący obiekt session do stworzenia tasku użyj metody
session.dataTaskWithURL(<url: NSURL>, completionHandler: <(NSData?, NSURLResponse?, NSError?) -> Void>)

Obsłuż response uwzględniając przypadki:

a) pełna serializacja danych zwróconych przez API
b) błędna serializacja danych zwróconych przez API

Do parsowania błędów zwróconych przez API użyj metody createNSErrorFromJson(json: JSON?) -> NSError?
