# Сценарий использования БД «Музей»
#### GEEKBRAINS, АМИНЕВ ИЛЬШАТ, 2023

## Ведение каталога экспонатов
База данных позволяет вести учет следующих параметров экспонатов музея:
* Инвентарный номер: номер, присвоенный экспонату в соответствии с внутренними правилами музея. Может быть составным, например: «102.22.55.А».
* Наименование: произвольное текстовое наименование.
* Описание: произвольное описание экспоната в текстовом виде.
* Собственный фонд: признак того, что экспонат является собственностью музея.
* Владелец: указывается для случаев, когда экспонат не является собственностью музея и принят на время – в рамках проведения какой-либо выставки. Выбирается из справочника «Контрагенты».
* Коллекция: группирующий экспонаты по принципу принадлежности к какой-либо коллекции признак. Выбирается из справочника «Коллекции».
* Вид экспоната: ссылка на элемент классификатора «Общий классификатор музейных предметов».
* Место происхождения: ссылка на географическую местность, в которой произошел экспонат. Выбирается из справочника «Локации».
* Эпоха происхождения: ссылка на возможные периоды/эпохи, может быть произвольным в зависимости от специфики музея: «палеозой», «средние века», «начало 19 века» и т.д. Выбирается из справочника «Эпохи».
* Год происхождения: указывается, если известен год происхождения.
* Материал: Указывается, из чего сделан экспонат. Выбирается из справочника «Материалы».
* Техника изготовления: Указывается, как сделан экспонат. Выбирается из справочника «Техники изготовления».
* Степень сохранности: оценка степени сохранности по 100-балльной шкале.
* Функциональное назначение: указывается, для чего применялся экспонат, если такое предусмотрено. Выбирается из справочника «функциональные назначения».
* Оценочная стоимость (+валюта): оценочная стоимость экспоната в указанной валюте. Актуально для коллекций, поступающих на временные экспозиции из-за рубежа / при передаче экспонатов за рубеж. Для валют ведется история курсов валют, чтобы можно было пересчитать в рубли – и таким образом, например получить оценочную стоимость всех фондов музея в необходимых разрезах.
* Условия хранения: указываются допустимые для экспозиции и хранения экспоната условия (температура, влажность, освещенность). Выбирается из справочника «Условия хранения»
* Способ экспозиции: обозначается, каким образом предпочтительно выставление экспоната, например: установлен на пол, повешен на стену, помещен под стекло, и т.д.
* Ширина, высота, глубина, вес: габариты и вес экспоната.
* QR_код: отдельно генерируемый код (GUID), предназначенный, к примеру, для печати на поясняющих табличках, расположенных рядом с экспонатами для последующего считывания мобильными телефонами. Использование внутренних кодов (или инвентарного номера) в данном случае не видится целесообразным, так как предоставление этих сведений в общий доступ может быть нежелательным для музея. Плюс, инвентарный номер может содержать кириллические символы, а это в ряде случаев вызывает проблемы при формировании QR-кодов.
* Используется: признак того, что экспонат используется и над ним могут быть произведены необходимые действия (то есть не выбыл из фонда).

Для экспонатов задается связанный с экспонатом медиаконтент: фото, видео, аудио материалы, также pdf-документы (и любые произвольные типы файлов). Контент может нумероваться, чтобы организовать показ в требуемом порядке – особенно актуально для фотогалерей.

## Ведение перечня помещений
Возможно ведение перечная корпусов, у каждого корпуса свой адрес. Помещения привязаны к корпусам, и для каждого помещения помимо названия ведется учет ряда характеристик, в частности, обеспечиваемые условия (температура, влажность, освещенность), высота потолков, площадь, наличие охраны. Также для каждого помещения указывается его предназначение: выставочный зал, склад, мастерская, конференц-зал и т.д. При размещении экспоната в помещении дополнительно указывается место.

## Движения фонда
### Прием экспонатов
Прием экспонатов отражается в «Книге поступлений основного фонда», в которой фиксируется когда, от кого, на каком основании (возмездно, на ответ.хранение или в подарок) получен тот или иной экспонат – с указанием ответственного сотрудника. При приеме также фиксируется первое движение экспоната с указанием операции (например, «Покупка») и фиксируется помещение и место размещения экспоната.

### Перемещение экспонатов
Все перемещения экспонатов между помещениями фиксируются с указанием помещения и места до и после перемещения, а также даты-времени и ответственного за перемещение сотрудника. Так что, по любому экспонату можно увидеть всю историю его перемещений.

### Консервация экспонатов
Экспонаты могут быть законсервированы, в таком случае они фиксируются в отдельной таблице. В любой момент можно посмотреть полный список законсервированных экспонатов в разрезе помещений. 

### Реставрация экспонатов
Экспонаты могут быть переданы на реставрацию, в таком случае они фиксируются в отдельной таблице. В любой момент можно ответить на вопросы «какой экспонат в каком помещении проходит реставрацию, кто именно из сотрудников и какие работы выполняет, как давно он там находится и когда плановое завершение». Также ведется история всех реставраций экспоната.

### Передача экспонатов на ответственное хранение
Передача экспонатов на ответственное хранение ведется в разрезе экспонатов и контрагентов. Фиксируется дата и время передачи, оценочная стоимость и ответственный сотрудник. Кроме того, указывается плановая дата возврата экспоната от контрагента.

### Прием экспонатов на ответственное хранение
Прием экспонатов на ответственное хранение ведется в разрезе экспонатов и контрагентов. Фиксируется дата и время приема, оценочная стоимость и ответственный сотрудник. Кроме того, указывается плановая дата возврата экспоната контрагенту.

## Экскурсии
Система позволяет вести перечень экскурсий. Для каждой экскурсии задается наименование, описание, список целевых аудиторий, стоимость и график проведения.

Также для каждой экскурсии фиксируется список сотрудников-экскурсоводов, которые могут ее провести.

У каждой экскурсии есть маршрут, в котором указываются точки маршрута в привязке к помещениям и экспонатам, с поясняющим текстом. С учетом того, что экскурсии можно делать для разных целевых аудиторий, описание также может отличаться – детям интересно одно, посетителям постарше другое.

К каждой точке маршрута можно привязать необходимо количество медиаконтента из карточки экспоната – опять-таки для разных целевых аудиторий это могут быть разные медиаданные.

## Продажи билетов
Структура базы данных позволяет вести учет продаж билетов с учетом льготных категорий посетителей. Для каждой льготной категории задается величина скидки в процентах, и происходит пересчет базовой стоимости билета в конечную.

Также ведется учет продаж экскурсий, с фиксацией экскурсовода, что позволит произвести дополнительные начисления сотруднику за проведенные экскурсии.

## Аренда аудиогидов
В системе ведется перечень аудиогидов, предназначенных для сдачи в аренду посетителям. Для каждой модели аудиогида назначается стоимость аренды и залоговая стоимость.

В журнале учета аренды аудиогидов ведется учет времени выдачи и возврата аудиогида, а также сумма полученной оплаты за аренду.
