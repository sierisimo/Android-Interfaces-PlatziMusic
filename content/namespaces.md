# XML, Namespace

Antes de arrancar directamente con los elementos de Android, debemos discutir un poco la estrcutra de un XML y entender que hace Android
internamente cuando encuentra algunos datos en el XML.

## XML

XML es un lenguaje que busca generar estructuras por tags. Esto es algo que ya conocemos. Sin embargo ciertos programas pueden tener
una interpretacion especifca para ciertos tags o atributos.

Sabemos que en XML la estrucutra de un tag puede tener dos formas:

```xml
<TAG_NAME></TAG_NAME>

o

<TAG_NAME />
```

La diferencia entre estas dos formas, reside en si el tag tendra un contenido interno o no.

Sin embargo, tanto el nombre del tago como el nombre de las atributos puede venir en dos formas:

```
NAME

o 

NAMESPACE:NAME
```

## Namespace

La diferencia entre estas dos formas esta en que al agregar un `NAMESPACE` estamos definiendo que este tag o atributo tiene un significado para algun programa en especifico.

Es decir, `NAMESPACE` refiere a que alguien nos define como se comporta este elemento, es decir, contextualiza el significado.

Pongamos un ejemplo de la vida real:

> Si yo te pregunto en este momento por Mariana. ¿Que me responderias?
> La respuesta va a variar de muchas maneras.
>
> - ¿Conocemos tu y yo a la misma Mariana?
> - ¿Estoy preguntando por Mariana mi compañera de clase o Mariana mi compañera de trabajo?
> - ¿Es acaso Mariana una persona o un nombre clave para un proyecto?

La idea de este ejemplo es explicar que un namespace es escencialmente describir donde un nombre tiene un significado. Si definieramos que el namespace de donde hablamos es la escuela, podriamos entonces responder rapidamente la pregunta sobre Mariana.

En XML es muy similar, al usar un namespace, definimos donde un nombre tiene significado o de que caso en especifico estamos hablando:

```xml
<school:person name="Mariana" />

<person job:id="12345">
```

## Namespaces en Android

En el caso concreto de Android, comunmente estaremos usando un namespace para los atributos de nuestra interfaz de usuario. Esto es porque el
SDK de android se encargara de usar este namespace para resolver valores
de interfaz de usuario y podes ajustar los elementos en pantalla.

Dicho namespace es meramente: `android`:

```xml
<TextView
    android:text="Hola App"
/>
```

Sin embargo, algunas librerias y utilidades de Android incluyen su propio namespace, por ejemplo, en el caso de los elementos de `AppSupport` (las librerias para compatibilidad) existe un namespace que comunmente se conoce como `app`.

## Resolucion de Namespaces

Para poder definir quien conoce el significado de un dato en un namespace es necesario indicar en nuestro XML un identificador unico de quien resuelve el namespace, comunmente definido por una dirección web aunque este valor puede ser cualquier URI valida:

```xml
<MyXML xmlns:platiz="http://platzi.com">
    <course platiz:name="Android UI" />
</MyXML>
```

En Android, los namespaces refieren a `http://schemas.android.com/` dependiendo el recurso. El namespace principal de Android es:

`xmlns:android="http://schemas.android.com/apk/res/android"`

Este namespace lo utiliza Android para hacer el calculo de las atributos de sus elementos en pantalla.
Otros namespaces pueden tener otras URI, mas adelante hablaremos de dos muy comunes.

En el ejemplo:

```xml
<TextView
    android:text="Hola App"
/>
```

Android reconoce que `text` representa una atributo de un `TextView` e internamente notifica a la clase `TextView` que recibio un valor para `text`. La clase `TextView` sabe que hacer con dicho valor (poner el texto en pantalla).
