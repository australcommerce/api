La API de Austral Commerce
==========================

Esta es una API REST que usa OAuth y devuelve datos en formato JSON.

## Hacer una solicitud
Todas las URLs comienzan con http://api.australcommerce.com.ar/v1/
Para hacer una solicitud y obtener datos usted tendría que hacer lo siguiente en curl:
curl -H 'authentication: ACCESS_TOKEN ' /
  https://api.australcommerce.com.ar/v1/order/000001
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

Es su responsabilidad en todos estos casos para reintentar la solicitud posterior.

## Tipo de Limitaciones
Usted puede realizar hasta 500 solicitudes por 5 minutos desde la app. Si usted excede este límite, obtendrá la siguiente error 429 Too Many Requests respuesta por posteriores solicitudes. Nosotros usamos los siguientes headers para proveer información:

• X-Rate-Limit-Limit : Total requests that con be done in a given period.

• X-Rate-Limit-Remaining : Remaining requests in the current period.

• X-Rate-Limit-Reset : Remaining seconds for the start of the next period.

## Paginación

## Metodos HTTP

Donde sea posible, la API vi se esfuerza para usar apropiadamente HTTP verbs para cada acción:
* HEAD :  Puede ser emitida en contra de cualquier recurso para obtener sólo la información de la cabecera HTTP.
* GET : Usado para recuperar recursos.
* POST : Usado para crear recursos.
* PUT : Se utiliza para la sustitución de recursos o colecciones. Para peticiones PUT sin atributo, asegúrese de configurar el encabezado Content-Length a cero.
* DELETE : Usado para eliminar recursos.

## Recursos de la API
### Datos generales
#### Autenticación
Host: api.australcommerce.com.ar

Authentication: [instancia]:[token]

Cache-Control: no-cache

### Cliente
#### Recuperar un Cliente
Recupera los datos de un cliente por su “nombre de usuario”.

#### Método
GET /v1/customer/{nombre_del_cliente}
 
#### Resultado
```
{
  userName: "consumidor"
  email: "support@australnova.com"
  identificationType: "CUIT"
  identificationNumber: null
  company: "Austral Commerce (directo)"
  address: "-"
  phone: "-"
  fax: null
  city: "-"
  province: "-"
  taxableKind: null
  deliverThru: null
  zip: "-"
  code: null
  priceList: null
  discount: 0
  enabled: true
  enabledPrice: true
  created: "2014-07-02T17:01:29.58"
  updated: "2014-12-04T22:57:13.363"
}
```

### Orden
#### Leer datos de una Orden
Recuperar datos de un Orden (pedido, cotización o compra directa), por su “número”.

#### Método
GET /v1/order/{numero_de_roden}
 
#### Resultado
```
{
  number: "000009"
  created: "2014-12-04T23:54:23.017"
  customer: 
  {
    code: null
    userName: "soporte"
    email: "development@australnova.com"
  }
  comments: null
  discount: 0
  status: "Pagado"
  history: 
  [6]
    0:  
    {
      at: "2014-12-05T00:05:34.737"
      status: "Pagado"
    }
    1:  
    {
      at: "2014-12-05T00:05:27.22"
      status: "Pagado"
    }
    2:  
    {
      at: "2014-12-04T23:57:24.677"
      status: "Cotizado"
    }
    3:  
    {
      at: "2014-12-04T23:55:27.673"
      status: "En Proceso de Cotizar"
    }
    4:  
    {
      at: "2014-12-04T23:54:55.767"
      status: "Cotizar"
    }
    5:  
    {
      at: "2014-12-04T23:54:23.563"
      status: "Pendiente"
    }
  payments: 
  [1]
    0:  
    {
      created: "2014-12-05T00:05:34.957"
      kind: "mercado-pago"
      transaction: "1417737891"
      comments: null
    }
    items: 
  [2]
    0:  
    {
    product: 
    {
      code: "PR045"
      name: "Producto de prueba"
    }
    quantity: 
    {
      ordered: 12
      original: 0
    }
    -
    total: 131.88
    price: 
    {
      ordered: 10.99
      original: 0
    priceChangeCauses: 
    [0]
  }
  kind: "Added"
  comments: 
    [1]
      0:  
      {
        at: "0001-01-01T00:00:00"
        origin: "external"
        comment: "de oferta esta semana. agregamos como acordamos por telefono."
      }
  variants: 
    [0]
  }
  1:  
  {
    product: 
  {
    code: "PR0374"
    name: "Producto de prueba"
  }
  quantity: 
  {
    ordered: 10
    original: 12
  }
  total: 2136.2
  price: 
  {
    ordered: 213.62
    original: 0
  priceChangeCauses: 
    [0]
  }
    kind: "Original"
  comments: 
  [1]
    0:  
    {
      at: "0001-01-01T00:00:00"
      origin: "external"
      comment: "como hablamos, el mínimo para este artículo es 10, no 12."
    }
  variants: 
  [0]
  }
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
  Code: "PR04423"
  Name: "Producto de prueba"
  Description: ""
  IsVisible: true
  IsEnabled: true
  ExternalCode: null
  Views: 0
  IsNew: false
  IsSale: false
  IsBold: false
  Brand: 
  {
    Name: "Marca 25"
    Description: ""
    Code: "16"
  }
  Tags: 
  [1]
    0:  
    {
      Name: "Etiqueta 70"
      Description: ""
      Code: "18"
    }
  Variants: 
  [0]
  Props: 
  [0]
  Prices: 
  [3]
    0:  
    {
      PriceList: "1"
      Regular: 102.03
      Sale: 0
    }
    1:  
    {
      PriceList: "2"
      Regular: 132.639
      Sale: 0
    }
    2:  
    {
      PriceList: "3"
      Regular: 0
      Sale: 0
    }
  Images: 
  [0]
}
```

## Ayudanos para hacer lo mejor
Por favor háganos saber cómo podemos mejorar la API. Si usted tiene una pregunta específica sobre una solicitud o si usted encontró un error, siéntase libre de expresarlo.

Se puede comunicar al siguiente email api@australcommerce.com.ar.
