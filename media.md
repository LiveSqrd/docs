#Media Api

Routes:
----
* [/media/get/:file](#media-get)
* [/media/save/:file](#media-save)
* [/media/upload](#media-upload)
* [/media/list](#media-list)

params
---
* w || width |Number| (Width in pixels)
* h || height |Number| (Height in pixels)
* x |Number| (x in pixels)
* y |Number| (y in pixels)
* crop |Boolean| (true requires w-h-x-y)
* strech |Boolean| (true requires w-h)
* q || quality |Number| (range 0-100)
* g || gravity |String| (used in crop North - NorthEast - NorthWest - East - West - South - SouthEast - SouthWest)
  
media-get
---
* route |GET| (/media/get/:file)
* file (ex: HIs83x9oS.jpg)
* query: [params](#params) (ex: ?w=100&h=100&strech=true)


media-save
---
* route |GET| (/media/save/:file) 
* file (ex: HIs83x9oS.jpg)
* query: [params](#params) (ex: ?w=100&h=100&strech=true)

Will create a variant, and save to media object making the modified path for recieving it with /media/get/:file.

media-upload
---
* route (/media/get/:file)
* file (ex: HIs83x9oS.jpg)
* post:
  * [params](#params) (ex: {w:100,h:100,strech:true})
  * file Field
    * mutlipart upload
    * base64 image |String|
  * name Field (if base64 the file needs a name with extendsion)
  
