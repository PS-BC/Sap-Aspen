# Servicio Bancor *'Abono a Cartera'*

Servicio mediante arquitectura [Rest](https://es.wikipedia.org/wiki/Transferencia_de_Estado_Representacional) en formtato [Json](https://es.wikipedia.org/wiki/JSON) que permitirá la comunicación de componentes externos hacia **BANCOR** para realizar la transacción 413 abono a cartera.

## Notas de la versión
Versión actual del servicio
> **1.0 - 19 Mayo del 2018 - William Ferro**

## Cambios en la versión
Lista de cambios realizados en la versión
+ Versión Inicial.

## Documentación del servicio

+ **Url del servicio**: Según configuración del servidor WEB en donde se alojara el servicio +
WSR_Financieras.dll/datasnap/rest/TServerMethodsFinancieras/TranFinan.

 + **Tipo de método [HTTP](https://es.wikipedia.org/wiki/Protocolo_de_transferencia_de_hipertexto)**  ***POST*** 

+ **Cabeceras Http [Headers](https://es.wikipedia.org/wiki/Anexo:Cabeceras_HTTP)**  **NO APLICAN**
+ **El mensaje en formato JSON sera incluido en el BODY del mensaje HTTP**


## Ejemplo de una solicitud *'Request'*
 
JSON en el BODY
    

   

    {
      "DatosBasicos": {
        "Canal": "22",
        "TipHor": "0",
        "DirIPOri": "127.0.0.1",
        "DirIPDes": "128.0.0.1",
        "PtoIPDes": "1234",
        "DirIPSer": "129.0.0.1",
        "PtoIPSer": "4567",
        "MaqOri": "ninguna",
        "MaqDes": "otra",
        "Aplicacion": "CAJASAP",
        "CodEntOri": "01",
        "FecTraOri": "2018-03-07",
        "HorTraOri": "15:34:78",
        "SecOri": "125348904",
        "SecRev": "",
        "NumPet": "1",
        "CodUsu": "CAJASAP",
        "CodTra": "413",
        "CodCau": "09",
        "CodSub": "00"
      },
      "DatosEntrada": {
        "NumProdTrn": "4200053716",
        "ValTotalTrn": "100000",
        "ValAboCuoTrn": "50000",
        "ValAboExtraTrn": "0",
        "TipAboExtraTrn": "1",
        "FecRecaudo": "2018-03-07"
      }
    }
    
## Descripción de la solicitud para la transaccion 413 de cartera *'Request'*


|Nombre del campo| Descripción | Tipo de dato | Longitud | Requerido| Formato|
|--|--|--|--|--| --|
| Canal| Código de canal de origen (el que se asigne a SAP) |String | 2 | Si|
| TipHor| Horario en el que se realiza la transaccion 0 = Normal, 1 = Adicional |String|1|Si| Siempre 0
| DirIPOri| Dirección IP de la maquina del usuario que origina la transacción |String | 20 |No|0.0.0.0|
| DirIPDes| Dirección IP del próximo destino|String | 20 |No|0.0.0.0|
| PtoIPDes | El puerto próximo de destino |String | 5 |No|
| DirIPSer| Dirección IP de la máquina del servidor |String|20|No|
| PtoIPSer| Puerto de la maquina del servidor |String | 5 |No|
| MaqOri| Nombre de la maquina que origina la transacción |String|16|No|
| MaqDes| Nombre de la maquina destino de la transacción |String | 16 |No|
| Aplicacion| Nombre de la aplicación que origino la transacción |String|20|No|
| CodEntOri| Código de la Entidad origen de la transacción |String | 2 |Si|
| FecTraOri | Fecha en la que se realiza la transacción |String|10|No|YYYY-MM-DD
| HorTraOri| Hora en la que se realiza la transacción |String | 8 |No|HH:MM:SS|
| SecOri| Secuencia única que identifica la transacción|String|30|Si|
| SecRev| Secuencia única que identifica la transacción a reversar |String | 30 |No|
| NumPet| Numero de peticiones que se ha realizado a la misma transacción|String|1|Si|
| CodUsu| Identificación del usuario que realiza la transacción |String | 12 |Si|
| CodTra| Código de la transacción a realizar|String|3|Si| Siempre 413
| CodCau| Código de causal de la transacción a realizar|String | 2 |Si| Siempre 09
| CodSub| Código de subcausal de la transacción a realizar|String | 2 |Si|siempre 00
| NumProdTrn| Numero del producto de cartera BANCOR|String | 10 |Si
| ValTotalTrn| Valor total de la transacción  |String|20|Si|#####.## decimal opcional
| ValAboCuoTrn| Valor que sera abonado a las cuotas del producto |String|20|Si|#####.## decimal opcional
| ValAboExtraTrn| Si el valor total es mayor al valor de las cuotas, se debe incluir el valor restante como abono extra |String|20|Si|#####.## decimal opcional
| TipAboExtraTrn| En caso de que se incluya valor en abono extra, se deberá incluir el tipo de abono extra, 1 = Disminución plazo, 2 = Disminución Cuota 3 = a Cuotas |String|1|Si
| FecRecaudo| Fecha efectiva del recaudo|String|10|No|YYYY-MM-DD




## Ejemplo de la respuesta de la solicitud *'Response'* 

La Información de respuesta del Api se encuentra en formato [Json](https://es.wikipedia.org/wiki/JSON)


    {
      "RespuestaBasica": {
        "FecPro": "2018-03-07",
        "SecOri": "1253458904",
        "CodTra": "413",
        "CodCau": "09",
        "CodSub": "00",
        "CodErr": "255",
        "MsjErr": "Transacción exitosa <Código 255>"
      }
    }



## Descripción de la respuesta de la solicitud *'Response'*
Esta información identifica la descripción completa de los campos de respueta por parte del servicio

|Nombre del campo| Descripción | Tipo de dato | Longitud Máxima| Formato |
|--|--|--|--|--|
| FecPro| Fecha en la que se realiza la transaccion |String | 10 |YYYY-MM-DD|
| SecOri| Secuencia única que identifica la transacción |String|30
| CodTra| Código de la transacción que se realizo |String|3
| CodCau| Código de causal de la transacción que se realizo |String|2
| CodSub|  Código de subcausal de la transacción que se realizo |String|3
| CodErr| Codigo que identifica el resultado de la transaccion |String|4
| MsjErr| Nombre detallado del código de la respuesta |String|30



## Códigos de Error y Estados de respuesta del servicio

A continuación encontrarás la definición de los códigos de respuesta por parte del servicio, y la posible solución.

|       Código         |Descripción                          |Posible solución                         |
|----------------|-------------------------------|-----------------------------|
|404| La url del servicio es invalida            |Verificar en la documentación la información del la url asignada para el consumo de esta|
|255          |Solicitud realizada satisfactoriamente|N/A|
|503          |La configuración del servicio presenta inconsistencias |Validar con el proveedor del servicio dicha inconsistencia|
|NNNN|otros posibles codigos de error generados por los servivios de BANCOR ||

## Ejemplo de la respuesta con error

    {
       "RespuestaBasica":    {
          "CodErr": "1905",
          "MsjErr": "Datos inconsistentes"
       },
       "DetalleErrores":    [
                {
             "CodErr": "2546",
             "MsjErr": "Tipo de horario invalido <Código 2546>"
          },
                {
             "CodErr": "2547",
             "MsjErr": "Direccion IP origen invalida <Código 2547>"
          }
       ]
    }
    
## Glosario

A continuación encontrarás el glosario de palabras de este documento

|       Palabra|Descripción                          
|----------------|-------------------------------|
|Request| Solicitud de una petición|
|Response|Respuesta de la solicitud|
|Api|Interfaz de programación de aplicaciones|

> Notas: 

 - Este documento puede ser modificado dependiendo de los ajustes realizados a la versión del servicio.
 

© 2018 [Processa S.A.S](https://processa.com/)
	


