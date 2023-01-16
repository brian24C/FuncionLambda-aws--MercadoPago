## FuncionLambda-aws--MercadoPago

# Comenzando 🚀
Esta función se crea con el propósito de usarlo en lambda AWS.

- ¿Qué es una función lambda AWS?

Una función Lambda de AWS es un servicio de AWS que permite ejecutar código sin provisionar ni administrar servidores, es por ello que es llamada SERVERLESS (sin sevidor). Puedes crear una función Lambda y asociarla a una variedad de eventos, como una solicitud HTTP a través de Amazon API Gateway (Cómo se hizo en este caso). Cada vez que se activa el evento, AWS Lambda ejecuta automáticamente la función y gestiona todas las tareas necesarias para escalar la ejecución según la demanda.

- ¿Qué es API Gateway?

API Gateway actúa como una "puerta" a través de la cual los clientes pueden acceder a la funcionalidad de la función Lambda mediante solicitudes HTTP.

- ¿Qué hace esta función del repositorio? 

Conectarse a mercadoPago y crear un pago con la información que viene del fronted (token, payment_method_id, transaction_amount, email, numero de DNI etc ) y devolverme el status, status_detail y el id del pago.

# Ejemplo:

Código de fronted en TypeScript:
```python
onSubmit: async (cardFormData: any) => {
            const response = await fetch(
              "Aquí va tu API endpoint",
              {
                method: "POST",
                headers: {
                  "Content-Type": "application/json",
                },
                body: JSON.stringify(cardFormData),
              }
            );
            console.log("response", await response.json());
```
Es este código se observa que estoy haciendo un fetch enviando toda la data mediante POST.

Esta data (información del pago) al ser enviada al backend tiene el siguiente formato:

![Untitled](https://user-images.githubusercontent.com/109192347/212758748-8d82cfda-2952-4241-bb6a-d2836e0d6f2b.png)

Luego en mi función lambda usaré el siguiente código para guardar el pago:

```python
sdk.payment().create(payment_data)
```

La función lambda después de guardar el pago, retornará el status y el id del pago.
Este return de la funcion lambda se recepcionará en el fronted y al imprimir por consola se debe ver la siguiente información:
![Captura de pantalla 2023-01-16 152947](https://user-images.githubusercontent.com/109192347/212761008-2ef7b375-9d07-4082-b8f8-da82ba965bac.png)
