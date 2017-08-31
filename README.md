La API de Austral Commerce
==========================

La versión 1 (V1) de nuestra API REST, que usa una autenticación por header y devuelve datos en formato JSON. A medida que vayamos haciendo cambios o agreguemos funcionalidades, actualizaremos la versión solo si el cambio es disruptivo.

## Hacer una solicitud
Todas las URLs comienzan con http://api.australcommerce.com.ar/v1/
Para hacer una solicitud y obtener datos tendrías que hacer lo siguiente en curl:
```
curl -H 'authentication: ACCESS_TOKEN ' /
  https://api.australcommerce.com.ar/v1/order/000001
```
donde el  ACCESS_TOKEN en el token para tener acceso a la API.

## Errores del Cliente

Estos son los posibles tipos de errores de la llamada a la API:

* Si los datos no existen retorna el siguiente error.
HTTP/1.1 404 Not found
 
_Empty_

* Si el token no es correcto o no existe retorna el siguiente error.
HTTP/1.1 401 Unauthorized
 
_Empty_

* Enviando por un método que no es utilizado para una solicitud retorna el siguiente error.
HTTP/1.1 405 Method no allowed
 
_{ Message: "The requested resource does not support http method 'POST'." }_

## Errores del Servidor
500 app is entirely down

502 Bad Gateway

503 Service Unavailable

504 Gateway Timeout. 

Es tu responsabilidad en todos estos casos reintentar una solicitud posterior.

## Metodos HTTP

Donde sea posible, la API vi se esfuerza para usar apropiadamente HTTP verbs para cada acción:
* HEAD :  Puede ser emitida en contra de cualquier recurso para obtener sólo la información de la cabecera HTTP.
* GET : Usado para recuperar recursos.
* POST : Usado para crear recursos.
* PUT : Se utiliza para la sustitución de recursos o colecciones. Para peticiones PUT sin atributo, asegúrete de configurar el encabezado Content-Length a cero.
* DELETE : Usado para eliminar recursos.

## Recursos de la API
### Datos generales
#### Autenticación
Host: api.australcommerce.com.ar

Authentication: [instancia]:[token]

Cache-Control: no-cache

Para utilizar la demo podes usar la siguiente autenticación:

Authentication: Demo-AustralCommerce:82a3bcb7fa23577d28d8422df13ac7470a734475a75bc8d28e16c9c1226d36b3

Para **Producción**, tenes que pedir los datos a la mesa de ayuda en hola@australcommerce.com.ar

### Cliente
#### Recuperar un Cliente
Recupera los datos de un cliente por su “nombre de usuario”.

#### Método
GET /v1/customer/{nombre_del_cliente}
 
#### Resultado
```
{
	"userName":"consumidor",
	"email":"support@australnova.com",
	"identificationType":"CUIT",
	"identificationNumber":null,
	"company":"Austral Commerce (directo)",
	"address":"-",
	"phone":"-",
	"fax":null,
	"city":"-",
	"province":"-",
	"taxableKind":null,
	"deliverThru":null,
	"zip":"-",
	"code":null,
	"priceList":null,
	"discount":0.0,
	"enabled":true,
	"enabledPrice":true,
	"created":"2014-07-02T17:01:29.58",
	"updated":"2014-12-04T22:57:13.363"
}
```

### Orden
#### Leer datos de una Orden
Recuperar datos de un Orden (pedido, cotización o compra directa), por su “número”.

#### Método
GET /v1/order/{numero_de_orden}
 
#### Resultado
```
{
	"number":"000009",
	"created":"2014-12-04T23:54:23.017",
	"customer":
	{
		"code":null,
		"userName":"soporte",
		"email":"development@australnova.com"
	},
	"comments":null,
	"discount":0.0,
	"status":"Pagado",
	"history":
	[
		{
			"at":"2014-12-05T00:05:34.737",
			"status":"Pagado"
		},
		{
			"at":"2014-12-05T00:05:27.22",
			"status":"Pagado"
		},
		{
			"at":"2014-12-04T23:57:24.677",
			"status":"Cotizado"
		},
		{
			"at":"2014-12-04T23:55:27.673",
			"status":"En Proceso de Cotizar"
		},
		{
			"at":"2014-12-04T23:54:55.767",
			"status":"Cotizar"
		},
		{
			"at":"2014-12-04T23:54:23.563",
			"status":"Pendiente"
		}
	],
	"payments":
	[
		{
			"created":"2014-12-05T00:05:34.957",
			"kind":"mercado-pago",
			"transaction":"1417737891",
			"comments":null
		}
	],
	"items":
	[
		{
			"product":
			{
				"code":"PR045",
				"name":"Producto de prueba"
			},
			"quantity":
			{
				"ordered":12.0,
				"original":0.0
			},
			"total":131.880,
			"price":
			{
				"ordered":10.990,
				"original":0.0,
				"priceChangeCauses":[]
			},
			"kind":"Added",
			"comments":
			[
				{
					"at":"0001-01-01T00:00:00",
					"origin":"external",
					"comment":"de oferta esta semana. agregamos como acordamos por telefono."
				}
			],
			"variants":[]
		},
		{
			"product":
			{
				"code":"PR0374",
				"name":"Producto de prueba"
			},
			"quantity":
			{
				"ordered":10.0,
				"original":12.0
			},
			"total":2136.200,
			"price":
			{
				"ordered":213.620,
				"original":0.0,
				"priceChangeCauses":[]
			},
			"kind":"Original",
			"comments":
			[
				{
					"at":"0001-01-01T00:00:00",
					"origin":"external",
					"comment":"como hablamos, el mÃ­nimo para este artÃ­culo es 10, no 12."
				}
			],
			"variants":[]
		}
	]
}
```
### Producto
#### Recuperar un Producto
Recuperar datos de un Producto por su “código”.

#### Método
GET /v1/product/{codigo_del_producto}
 
#### Resultado

```
{
	"Code":"PR04423",
	"Name":"Producto de prueba",
	"Description":"",
	"IsVisible":true,
	"IsEnabled":true,
	"ExternalCode":null,
	"Views":0,
	"IsNew":false,
	"IsSale":false,
	"IsBold":false,
	"IsUnavailable": false,
	"Brand":
	{
		"Name":"Marca 25",
		"Description":"",
		"Code":"16"
	},
	"Tags":
	[	
		{
		"Name":"Etiqueta 70",
		"Description":"",
		"Code":"18"
		}
	],
	"Variants":[],
	"Props":[],
	"Prices":
	[
		{
		"PriceList":"1",
		"Regular":102.030,
		"Sale":0.0
		},
		{
		"PriceList":"2",
		"Regular":132.639,
		"Sale":0.0},
		{
		"PriceList":"3",
		"Regular":0.000,
		"Sale":0.0
		}
	],
	"Images":[]
}
```

## Ayudanos para hacerlo mejor
Por favor hacenos saber cómo podemos mejorar la API. Si tenes una pregunta específica sobre una solicitud o si encontraste un error, avisanos.

Carga un [Issue acá en Github](https://github.com/australcommerce/api/issues), o escribinos a hola@sucursalweb.io. En Twitter somos [@sucursalwebio](https://twitter.com/sucursalwebio)
