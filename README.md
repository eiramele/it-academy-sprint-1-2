# Patró de disseny Builder en TypeScript

## Introducció. Què són els patrons de disseny?

Els patrons de disseny són solucions generalitzades a problemes comuns en el disseny de software. Són com plantilles que es poden personalitzar per adaptar-se a les necessitats específiques del codi. Els patrons de disseny poden facilitar la comprensió del codi, ja que proporcionen una manera estàndard de resoldre problemes coneguts.

Hi ha tres tipus principals de patrons de disseny:

1. **Patrons creacionals**: Aquests patrons se centren en maneres de crear objectes o classes. L'objectiu és separar el codi que s'encarrega de la creació i la manipulació dels objectes. Alguns d'aquests patrons són: Singleton, Factory, Abstract Factory, Builder, Prototype.

2. **Patrons estructurals**: Aquests patrons es preocupen per la composició de classes i objectes. Busquen simplificar l'estructura i promoure la reutilització de codi. Alguns d'aquests patrons són: Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy.

3. **Patrons de comportament**: Aquests patrons s'encarreguen de la comunicació efectiva i l'assignació de responsabilitats entre objectes. Exemples: Chain of Responsibility, Command, Interpreter, Iterator, Mediator, Memento, Observer, State, Strategy, Template Method, Visitor.


## Descripció de Builder

El patró de disseny Builder és un patró creacional que permet construir objectes complexos pas a pas. Es pot utilitzar per crear una configuració d'objectes diferents.

![Builder Pattern](https://integu.net/wp-content/uploads/2020/11/INTEGU-builder-design-pattern-overview-768x432.png)

(Font: integu.net)

Aquest patró permet la construcció d'un objecte complex utilitzant passos simples. El patró Builder construeix l'objecte final pas a pas i aquesta construcció és independent del procés de representació.

El patró Builder fa que es tregui el codi de construcció de l'objecte de la seva pròpia clase i es col·loqui dins d'objectes independents, anomenats "constructors". D'aquesta manera s'evita que es creï una classe amb un grup de subclasses o que es creï un constructor gegants amb molts paràmetres.

Així, quan es crea un objecte nou s'executen una sèrie de passos del constructor, però no cal invocar-los tots.

## Classe directora
També es poden extreure una sèrie de crides als passos del constructor que es fa servir per construir un procudcte i posar-les en una classe independent, que s'anomena "dirctora". Aquesta classe defineix l'ordre en què s'han d'exectura els passos de construcció, mentre que el constructor proporciona la implementació d'aquests passos.

## Estructura
1. Interfície constructora: declara els passos de construcció
2. Constructors concrets: ofereixen les diferents implementacions dels passos de construcció. Poden crear productes que no siguin de la interfície comuna.
3. Productes: són els objectes resultants. No cal que pertanyin a la mateixa jerarquia de classes o interfície.
4. Classe directora: defineix l'ordre en què s'invocaran els passos.
5. Client: ha d'associar un dels objectes constructors a la classe directora.


![Builder Pattern](https://refactoring.guru/images/patterns/diagrams/builder/structure-2x.png)

(Font: Refactorging.guru)

## Avantatges
1. Es construeix el codi pas a pas.
2. Es reutilitza el codi i es poden construir objectes molt diferents amb un sol bloc de codi.
3. Principi de responsabilitat única: es pot aïllar el codi de construcció del codi de funcionalitats de l'objecte.

## Desavantatges
La complexitat del codi augmenta, perquè el patró escull la creació de múltiples classes.


## Exemple de codi

Aquest és un exemple de com es pot utilitzar el patró Builder amb TypeScript:

```typescript
class Builder {
    private product: Product;

    constructor() {
        this.reset();
    }

    public reset(): void {
        this.product = new Product();
    }

    public buildStepA(): void {
        // implementació del pas A
    }

    public buildStepB(): void {
        // implementació del pas B
    }

    public getProduct(): Product {
        const result = this.product;
        this.reset();
        return result;
    }
}

class Product {
    public listParts(): void {
        console.log('Product parts...');
    }
}

const builder = new Builder();
builder.buildStepA();
builder.buildStepB();
const product = builder.getProduct();
product.listParts();
