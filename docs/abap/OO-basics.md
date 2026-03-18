---
layout: page
title: Additions to object orientation
permalink: /abap/oo-basics/
parent: Design and design of modern SAP applications
grand_parent: Moderne ABAP Entwicklung
nav_order: 1
---

1. TOC
{:toc}

{: .no_toc}
# Additions and details on object orientation topics

Here you will find additional information on the topics of object orientation:

## Basic principles of object orientation (SOLID) - addition

<dl>
  <dt>Single Responsibility Principle</dt>
  <dd>
    A code unit (class, method, ...) should always have a purpose and therefore a reason for adjustments. A method that...
    Reading Customizing entries, using them to prepare data, and then outputting a form has three purposes and also possible reasons for
    Adjustments (namely whenever something needs to change in Customizing/data/form). So this method should be split.
  </dd>

  <dt>Open/Closed Principle</dt>
  <dd>
    A module should be open to extensions and closed to changes. This means that adjustments can be made without
    For example, to edit the class originally used. A class `Drucker`, which obtains the data to be printed in the constructor, can
    will not print anything else without adapting the original code. However, this class gets an instance of the interface `Datenbeschaffung` in
    Constructor passed and calls appropriate methods of this, a second data retrieval class can easily be developed for customization.
  </dd>

  <dt>Liskov Substitution Principle</dt>
  <dd>
    Code that works with a class or interface should always work with implementing or inheriting classes. An inheriting class
    For example, it should not throw an unexpected exception in one of the implemented methods and thus trigger a dump.
  </dd>

  <dt>Interface Segregation Principle</dt>
  <dd>
    Interfaces should be divided in such a way that users only receive necessary dependencies. A database access class that is used in an application
    can read and write data used, could implement an interface `Datenleser` and an interface `Datenschreiber`, so that
    Read-only users have no dependency on writing methods.
  </dd>

  <dt>Dependency Inversion Principle</dt>
  <dd>
    Dependencies such as the instance of a class that implements the interface `Datenbeschaffung` should not be replaced by a class using `Anzeiger`
    be created, but instead passed to the constructor or a method. So to test `Anzeiger` you can simply use another one
    Implementation for data collection will be handed over.
  </dd>
</dl>

## Design patterns

Here you will find additional explanations of the most important design patterns:

### Singleton-Pattern

The singleton pattern aims to ensure that only a single object instance exists or can exist for a class at runtime. To do this, the first instance created by the constructor is written into a class variable (CLASS-DATA) and in subsequent calls to the class constructor to create a new object, this saved instance is read from the class variable and returned. This way you can control that only one instance of a class exists at any time.
Here is an example of how this could be implemented:

```
CLASS zcl_singleton DEFINITION.
  PUBLIC SECTION.
    CLASS-METHODS:
      get_instance RETURNING VALUE(instance) TYPE REF TO zcl_singleton.
    METHODS:
      do_something.
  PRIVATE SECTION.
    CLASS-DATA:
      instance_ref TYPE REF TO zcl_singleton.
    METHODS:
      constructor.
ENDCLASS.

CLASS zcl_singleton IMPLEMENTATION.
  METHOD constructor.
    " Konstruktor ist privat, um direkte Instanziierung zu verhindern
  ENDMETHOD.
  METHOD get_instance.
    IF instance_ref IS INITIAL.
      CREATE OBJECT instance_ref.
    ENDIF.
    instance = instance_ref.
  ENDMETHOD.
  METHOD do_something.
    WRITE: / 'Singleton-Methode wurde aufgerufen'.
  ENDMETHOD.
ENDCLASS.

* Verwendung
DATA(singleton) = zcl_singleton=>get_instance( ).
singleton->do_something( ).
```

### Factory-Pattern

The factory pattern is a design pattern that encapsulates the creation of objects. In ABAP it is often used to centralize and simplify the instantiation of objects - especially for polymorphic objects or when creation is complex. The pattern offers several advantages: changes to the creation logic only have to be made in one place, the return of an interface or an abstract class (polymorphism) is possible and new types can be easily added.
This could be implemented as follows:

```
* Abstrakte Basisklasse oder Interface
INTERFACE if_vehicle.
  METHODS drive.
ENDINTERFACE.

* Konkrete Implementierungen
CLASS zcl_car DEFINITION.
  PUBLIC SECTION.
    INTERFACES if_vehicle.
ENDCLASS.

CLASS zcl_car IMPLEMENTATION.
  METHOD if_vehicle~drive.
    WRITE: / 'Das Auto fährt los!'.
  ENDMETHOD.
ENDCLASS.

CLASS zcl_bike DEFINITION.
  PUBLIC SECTION.
    INTERFACES if_vehicle.
ENDCLASS.

CLASS zcl_bike IMPLEMENTATION.
  METHOD if_vehicle~drive.
    WRITE: / 'Das Fahrrad fährt los!'.
  ENDMETHOD.
ENDCLASS.

* Factory-Klasse
CLASS zcl_vehicle_factory DEFINITION.
  PUBLIC SECTION.
    CLASS-METHODS:
      create_vehicle
        IMPORTING type_name TYPE string
        RETURNING VALUE(vehicle) TYPE REF TO if_vehicle.
ENDCLASS.

CLASS zcl_vehicle_factory IMPLEMENTATION.
  METHOD create_vehicle.
    CASE type_name.
      WHEN 'CAR'.
        CREATE OBJECT vehicle TYPE zcl_car.
      WHEN 'BIKE'.
        CREATE OBJECT vehicle TYPE zcl_bike.
      WHEN OTHERS.
        vehicle = NULL.
    ENDCASE.
  ENDMETHOD.
ENDCLASS.

* Verwendung
DATA(vehicle) = zcl_vehicle_factory=>create_vehicle( type_name = 'CAR' ).
IF vehicle IS BOUND.
  vehicle->drive( ).
ENDIF.
```

### Facade-Pattern

The Facade pattern is used in ABAP to provide a simplified interface to a complex subsystem. It encapsulates the complexity of multiple classes or processes behind a single, easy-to-use class - the “facade”. This offers the following advantages: The caller does not have to deal with details of the subsystems, changes in the subsystems do not directly affect the calls and the facade can be reused in different contexts.
This could be implemented as follows:

```
* Subsystem-Klassen
CLASS zcl_order_processor DEFINITION.
  PUBLIC SECTION.
    METHODS process_order.
ENDCLASS.

CLASS zcl_order_processor IMPLEMENTATION.
  METHOD process_order.
    WRITE: / 'Bestellung verarbeitet'.
  ENDMETHOD.
ENDCLASS.

CLASS zcl_invoice_generator DEFINITION.
  PUBLIC SECTION.
    METHODS generate_invoice.
ENDCLASS.

CLASS zcl_invoice_generator IMPLEMENTATION.
  METHOD generate_invoice.
    WRITE: / 'Rechnung erstellt'.
  ENDMETHOD.
ENDCLASS.

CLASS zcl_shipping_service DEFINITION.
  PUBLIC SECTION.
    METHODS ship_order.
ENDCLASS.

CLASS zcl_shipping_service IMPLEMENTATION.
  METHOD ship_order.
    WRITE: / 'Versand durchgeführt'.
  ENDMETHOD.
ENDCLASS.

* Facade-Klasse
CLASS zcl_order_facade DEFINITION.
  PUBLIC SECTION.
    METHODS complete_order_process.
ENDCLASS.

CLASS zcl_order_facade IMPLEMENTATION.
  METHOD complete_order_process.
    DATA(processor) = NEW zcl_order_processor( ).
    DATA(invoice)   = NEW zcl_invoice_generator( ).
    DATA(shipping)  = NEW zcl_shipping_service( ).

    processor->process_order( ).
    invoice->generate_invoice( ).
    shipping->ship_order( ).
  ENDMETHOD.
ENDCLASS.

* Verwendung
DATA(facade) = NEW zcl_order_facade( ).
facade->complete_order_process( ).
```

### MVC-Pattern

The MVC pattern is used to divide the programming logic into three areas: Model (data model), View (presentation logic) and Controller (business logic).
The Model-View-Controller (MVC) pattern is a proven architectural model that can also be used in ABAP - especially in the context of SAP. It separates the application into three main components: "Model" (business logic and data access), "View" (representation of data / UI) and "Controller" (intermediation between Model and View).
The use of MVC offers the following advantages: Better maintainability and testability due to the separation of concerns, reusability of views and models, scalability for complex applications.

The Restful Application Programming Model represents the MVC pattern, as the technical framework already specifies a strict separation of concerns in the form of Model = CDS, Control = Behavior Definition and View = Fiori.

```
* Model Klasse
CLASS zcl_model DEFINITION.
  PUBLIC SECTION.
    METHODS:
      get_customer_name IMPORTING customer_id TYPE i RETURNING VALUE(customer_name) TYPE string.
ENDCLASS.

CLASS zcl_model IMPLEMENTATION.
  METHOD get_customer_name.
    CASE customer_id.
      WHEN 1. customer_name = 'Max Mustermann'.
      WHEN 2. customer_name = 'Erika Musterfrau'.
      WHEN OTHERS. customer_name = 'Unbekannt'.
    ENDCASE.
  ENDMETHOD.
ENDCLASS.

* View Klasse
CLASS zcl_view DEFINITION.
  PUBLIC SECTION.
    METHODS:
      display_customer_name IMPORTING customer_name TYPE string.
ENDCLASS.

CLASS zcl_view IMPLEMENTATION.
  METHOD display_customer_name.
    WRITE: / 'Kundenname:', customer_name.  "hier könnte auch eine ALV-Ausgabe o.ä. stehen
  ENDMETHOD.
ENDCLASS.

* Controller Klasse
CLASS zcl_controller DEFINITION.
  PUBLIC SECTION.
    METHODS:
      show_customer IMPORTING customer_id TYPE i.
  PRIVATE SECTION.
    DATA:
      model TYPE REF TO zcl_model,
      view  TYPE REF TO zcl_view.
ENDCLASS.

CLASS zcl_controller IMPLEMENTATION.
  METHOD show_customer.
    CREATE OBJECT model.
    CREATE OBJECT view.

    DATA(name) = model->get_customer_name( customer_id ).
    view->display_customer_name( name ).
  ENDMETHOD.
ENDCLASS.
```

Here, too, we unfortunately cannot go into all the design patterns in detail; on the Internet and in specialist literature you will find numerous opportunities to approach the topic and bring it into the organization. A good starting point for your own research is, for example, [ABAP-OO Design Patterns m. Beispielen](https://zevolving.com/category/abapobjects/oo-design-patterns/).