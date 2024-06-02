<div align="center">
<img src="https://github.com/edumel20/Markdown_Design/blob/main/Tareas_Factory/img/img_patron_factory.png?raw=true" width="700px"/>
</div>


# Implementación de Abstract Factory con python
## Concrete_factory.py

```python
from abstract_factory import UIABstractFactory, Button, Textbox

class DarkButton(Button):
    def paint(self):
        print("Dark Button")

class DarkTextbox(Textbox):
    def paint(self):
        print("Dark Textbox")

class LightButton(Button):
    def paint(self):
        print("Light Button")

class LightTextbox(Textbox):
    def paint(self):
        print("Light Textbox")

class DarkUIFactory(UIABstractFactory):
    def create_button(self):
        return DarkButton()

    def create_textbox(self):
        return DarkTextbox()

class LightUIFactory(UIABstractFactory):   
    def create_button(self):
        return LightButton()
    
    def create_textbox(self):
        return LightTextbox()
```

- `Button` y `Textbox` son las interfaces abstractas para los productos de botón y cuadro de texto, respectivamente.
- `DarkButton` y `DarkTextbox` son implementaciones concretas de los productos de botón y cuadro de texto para el tema oscuro.
- `LightButton` y `LightTextbox` son implementaciones concretas de los productos de botón y cuadro de texto para el tema claro.
- `UIAbstractFactory` es la interfaz abstracta para la fábrica abstracta que define los métodos para crear botones y cuadros de texto.
- `DarkUIFactory` y `LightUIFactory` son implementaciones concretas de fábricas abstractas que crean productos relacionados para los temas oscuro y claro, respectivamente.

Este patrón es útil cuando necesitas crear familias de productos relacionados sin especificar sus clases concretas, lo que proporciona flexibilidad para cambiar entre estas familias de productos fácilmente.

## Abstract_factory.py

```python
from abc import ABC, abstractmethod

class UIABstractFactory(ABC):
    @abstractmethod
    def create_button(self):
        pass

    @abstractmethod
    def create_textbox(self):
        pass

class Button(ABC):
    @abstractmethod
    def paint(self):
        pass

class Textbox(ABC):
    @abstractmethod
    def paint(self):
        pass
```

- `UIAbstractFactory`: Esta es la interfaz abstracta para la fábrica abstracta. Define métodos abstractos para crear diferentes tipos de productos, como botones y cuadros de texto.

- `Button` y `Textbox`: Estas son las interfaces abstractas para los productos específicos. Cada una define un método abstracto `paint()` que debe ser implementado por las clases concretas que representan los botones y cuadros de texto reales.

- `ABC` y `abstractmethod`: Estas son clases y decoradores proporcionados por el módulo `abc` de Python, que se utilizan para definir clases y métodos abstractos. Una clase que hereda de `ABC` se convierte en una clase abstracta, y un método decorado con `@abstractmethod` se convierte en un método abstracto que debe ser implementado por las clases derivadas.

Este código establece un conjunto de interfaces abstractas que deben ser implementadas por las clases concretas que representan las fábricas y los productos reales en tu sistema de interfaz de usuario. Esto sigue el principio de diseño de "programar hacia interfaces, no hacia implementaciones", lo que te permite cambiar fácilmente las implementaciones concretas sin modificar el código cliente.

## Main.py

```python
from concrete_factory import DarkUIFactory, LightUIFactory

def client_code(factory):
    button = factory.create_button()
    textbox = factory.create_textbox()

    button.paint()
    textbox.paint()

if __name__ == '__main__':
    client_code(DarkUIFactory())
    client_code(LightUIFactory())
```

Tu código principal (`client_code`) utiliza las fábricas concretas (`DarkUIFactory` y `LightUIFactory`) para crear objetos concretos (botones y cuadros de texto) y luego llama al método `paint()` en cada uno de ellos para "pintar" la apariencia de los componentes de la interfaz de usuario.

Aquí está el flujo del código:

1. `client_code`: Esta función toma una fábrica concreta como argumento y la utiliza para crear un botón y un cuadro de texto. Luego, llama al método `paint()` en cada uno de ellos.

2. `if __name__ == '__main__':` Esta línea asegura que el código dentro de este bloque solo se ejecute si este script es el programa principal.

3. `client_code(DarkUIFactory())`: Llama a `client_code` con una instancia de `DarkUIFactory`, lo que resulta en la creación de un botón y un cuadro de texto oscuros.

4. `client_code(LightUIFactory())`: Llama a `client_code` con una instancia de `LightUIFactory`, lo que resulta en la creación de un botón y un cuadro de texto claros.

Este código muestra cómo se pueden usar las fábricas concretas para crear diferentes familias de objetos relacionados (en este caso, botones y cuadros de texto) sin que el código cliente dependa de las clases concretas específicas de los productos. Esto ilustra el principio de diseño de "separación de preocupaciones", donde la creación de objetos y su uso se mantienen separados y modularizados.
