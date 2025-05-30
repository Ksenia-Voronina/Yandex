# Проект "Веб-ларек"

Стек: HTML, SCSS, TS.
Для сборки используется Webpack.

Структура проекта:
- src/ — исходные файлы проекта
- src/components/ — папка с JS компонентами
- src/components/base/ — папка с базовым кодом

Важные файлы:
- src/pages/index.html — HTML-файл главной страницы
- src/types/index.ts — файл с типами
- src/index.ts — точка входа приложения
- src/scss/styles.scss — корневой файл стилей
- src/utils/constants.ts — файл с константами
- src/utils/utils.ts — файл с утилитами

## Установка и запуск
Для установки и запуска проекта необходимо выполнить команды

```
npm install
npm run start
```

или

```
yarn
yarn start
```
## Сборка

```
npm run build
```

или

```
yarn build
```

## Описание базовых классов
### 1. Базовый класс `Api`
Класс Api отвечает за работу запросов к серверу. Его функции: получение и отправление данных на сервер.
Конструктор принимает такие аргументы: 
- baseUrl: string // базовая ссылка
- options: RequestInit = {} // настройки запроса
Класс имеет следудующие методы:
- handleResponse() // проверяет ответ от сервера
- get() // реализует метод 'GET'
- post() // реализует метод 'POST'

### 2. Базовый класс `Component<T>`
Данный класс является абстрактным классом компонента. Предназначен для созданяи компонентов пользовательского интерфейса. Конструктор принимает контейнер HTMLElement, где будет находиться компонент.
Класс обладает следующими методами:
- toggleClass() // переключает классы
- setText() //  устанавливает текстовое содержимое для элемента
- setDisabled() // меняет статус элемента на активный/неактивный
- setHidden() // скрывает элемент
- setVisible() // делает элемент видимым
- setImage() // устанавливает изображение с атрибутом alt
- render() // возвращает DOM-элемент

### 3. Базовый класс `EventEmitter`
Данный класс позволяет подписываться на события и уведомлять подписчиков о наступлении события.
Имеет следующие методы:
- on () // подписывает на событие
- off() // отписывает на событие
- emit() // уведомляет о событии
- onAll() // подписывает на все события
- ofAll() // отписывает от всех событий
- trigger() // генерирует заданное событие с заданными аргументами
 
### 4. Базовый класс `Model<T>`
Данный класс является абстрактным и представляет собой базовую модель. Конструктор принимает следующие аргументы:
- data: Partial<T> // частичные данные
- events: IEvents // события
Содержит метод emitChanges(), который оповещает о том, что модель изменилась.

## Классы модели данных
### 1. Класс `Product`
Данный класс представляет собой модель продукта, наследует функциональность от класса Model. Класс используется для здания и управдения данными продукта.
Имеет следующие свойства:
- id: string; // ID товара
- description: string; // описание товара
- image: string; // картинка товара
- title: string; // название товара
- category: string; // категория товара
- price: number; // цена товара

### 2. Класс `AppState`
Данный класс является наследником Model. Он хранит состояние приложения, каталог продуктов, корзину, заказ, данные для предварительного просмотра, ошибки формы. Использует интерфейс IAppState. Конструктор класса принимает начальное состояние приложения, а также инициализирует свойства класса catalog, basket, order, preview и formErrors.
Содержит следующие методы:
- clearOrder() // используется для очистки данных о заказе.
- setCatalog() // используется для установки каталога продуктов.
- setPreview() // используется для установки предварительного просмотра продукта.
- handleBasketAction() // используется для обработки добавления и удаления товара в корзине.
- clearBasket() // используется для удаления всех товаров из корзины.
- refreshBasket() // используется для обновления данных о корзине.
- setOrderField() // используется для установки значений полей заказа.
- setContactField() // используется для установки значений полей контактных данных.
- validateOrderForm() // используется для валидации данных заказа.
- validateContactForm() // используется для валидации данных контактных данных.
- handleBasketAction() // используется для добавления и удаления товара из корзины

## Классы компенентов представления
### 1. Класс `Modal`
Класс Modal обеспечивает работу модального окна и наследуется от Component<IModalData>. Его функции: открытие и закрытие модального окна с подробной  информацией.
Конструктор принимает `constructor(container: HTMLElement, protected events: IEvents)` - контейнер модального окна и объект для управления событиями. Также в конструкторе происходит инициализация кнопки закрытия окна и контейнера с контентом.
Включает в себя методы:
- set content // заменяет контент на значение
- open() // открывает модальное окно 
- close() // закрывает модальное окно 
- render() // возвращает контейнер

### 2. Класс `Form<T>`
Данный класс наследует класс Component. Конструктор принимает `constructor(container: HTMLFormElement, events: IEvents)` -  контейнер формы и объект для управлением событиями в качестве параметров, а также выполняет инициализацию _submit и _errors. Устанавливает обработчики события на ввод данных и отправку формы. Свойство valid устаналивает отключенное состояние для кнопки отправки формы. Свойство errors устанавливает текст ошибки.
Содержит следующие методы: 
- onInputChange() // следит за изменениями формы
- render() // отрисовывает форму
- set valid // управляет доступностью кнопки оптравки в зависимости от валидности формы.
- set errors // устанавливает и отображает ошибки валидации формы.

### 3. Класс `Basket`
Данный класс наследует Component. Конструктор принимает HTML-элемент и события. В нем инициализируется список товаров, итоговая сумма и кнопка. Также содержит функцию, которая добавляет обработчик событий на кнопку и возвращает массив товаров.
Класс имеет следующие свойства:
- items - устанавливает текст для пустой корзины или вставляет товары.
- total - устаналивает текст с итоговой суммой.

### 4. Класс `Success`
Класс является наследником Component. Конструктор принимает `constructor(container: HTMLFormElement, events: IEvents)` -  контейнер и объект для управлением событиями в качестве параметров. Выполняется инициализация _close и _description. Свойство description предоставляет доступ к содержимому элемента.
Класс имеет следующие методы: 
- get description() // получает текст описания
- set description() // устанавливает текст описания


### 5. Класс `OrderForm`
Данный класс является наследником класса Form и принимает обобщенный параметр IContactForm. Конструктор класса принимает контейнер формы, объект событий и объект actions, содержащий действия, выполняемые при нажатии на кнопку. Также устанавливаются обработчики событий клика на кнопки оплаты. 
Имеет следующие методы:
- addButtonClickHandler() / обрабатывает события клика на кнопки оплаты.
- toggleButtons() // измененяет визуальное состояние кнопок оплаты.
- address() // получает и устанавливает значение адреса в форме заказа.

### 6. Класс `ShopApi`
Данный класс является наследником класса Api. Конструктор принимает cdn, baseUrl и oprions.
Класс содержит следующие методы:
- getItemList() // возвращает массив товаров
- getItem() // возвращает один товар
- orderItems() // реализует функцию заказа

### 7. Класс `Card`
Данный класс является наследником класса Component. Конструктор класса принимает контейнер, в котором будет отображаться карточка, и действия, которые будут выполняться при клике на карточку или кнопку. 
Он имеет следующие свойства и методы:
- disableButton() // отключает кнопку при нулевой цене.
- id // устанавливает и получает идентификатор карточки
- buttonText // устанавливает текст кнопки.
- title // устанавливает и получает заголовок карточки.
- price // устанавливает и получает цену карточки.
- image // устанавливает и получает картинку карточки.
- category // устанавливает и получает категорию карточки.
- index // устанавливает и получает индекс карточки.

### 8. Класс `Page`
Данный класс наследуется от базового класса Component и принимает обобщенный параметр IPage. Конструктор класса принимает constructor(container: HTMLElement, events: IEvents) - контейнер страницы и объект для управлением событий. 
Имеет следующие свойства, методы и функции:
- функция ensureElement // инициализирует свойства с HTML-элементами.
- handleBasketClick() // обрабатывает события клика на элемент корзины.
- counter() // установка значения счетчика товаров в корзине.
- gallery() // установка элемента галереи товаров.
- locked() // установка состояния блокировки страницы.

### 9. Класс `Basket`
Данный класс является наследником Component<IBasketView>. Принимает обобщенный параметр IBasketView, который представляет тип данных для его состояния. Конструктор класса constructor(container: HTMLElement, events: EventEmitter) - принимает контейнер страницы и объект для управлением событий. Также устанавливаются обработчики событий клика на кнопку оформления заказа.
Содержит ряд методов, обработчиков и свойств:
- toggleButton() // включение/отключение кнопки оформления заказа.
- items() // устанавливает список элементов корзины.
- total() // установливает общую сумму заказа.

## Описание данных
Данные товара
```
interface IProduct {
    id: string; // ID товара
    description: string; // описание товара
    image: string; // картинка товара
    title: string; // наименование товара
    category: string; // категория товара
    price: number | null; // цена товара
}
```

Данные состояния приложения
```
interface IAppState {
    catalog: IProduct[]; // каталог товаров
    basket: string[]; // корзина
    preview: string | null; // прелпросмотр
    order: IOrder | null; // заказ
    loading: boolean; // загрузка
}
```

Данные формы заказа
```
interface IOrderForm {
    payment: string; // способ оплаты
    adress: string; // адрес получателя
}
```

Данные контактной формы
```
interface IContactForm {
    phone: string; // номер телефона получателя
    email: string; // электронная почта
}
```

Данные товаров в заказе
```
interface IOrder extends IOrderForm {
    items: string[]; // список товаров
}
```

Данные об ошибках в формах
```
type FormErrors = Partial<Record<keyof IOrder, string>>;
```

Данные итогового заказа
```
interface IOrderResult {
    id: string; // ID товара
}
```

Данные карточки товара
```
interface ICards extends IProduct {
    index?: string; 
    buttonTitle?: string;
}
```

Данные корзины
```
interface IBasketView {
    items: HTMLElement[]; // список товаров в корзине
    total: number; // итоговая сумма
}
```

Данные главной страницы
```
interface IPage {
    counter: number; // счетчик
    gallery: HTMLElement[]; // галерея
}
```

Данные событий
```
interface IActions {
    onClick: (event: MouseEvent) => void; // событие по клику
}
```