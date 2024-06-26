# اساسيات لغة Cairo

تُعد Cairo لغة العقد الذكي المستخدمة لتطوير العقود الذكية على شبكة StarkNet. الأهم من ذلك، Cairo هي لغة كاملة متوافقة مع STARK Proofs، وعلى الرغم من أننا نستخدمها في هذا السياق لبناء عقود ذكية على StarkNet، ويمكنك استخدامها خارج StarkNet كذلك! على عكس لغة Solidity، تم بناء لغة Cairo منذ اليوم الأول بهدف التوافق مع أنظمة إثبات ZK. لذلك، يمكن ترجمة أي معاملات لعقد ذكي مكتوب باستخدام لغة Cairo تلقائيًا وبكفاءة إلى دليل ZK-STARK الذي يمكن وضعه على الطبقة الأولى.

Cairo هي لغة برمجة ثورية لا مثيل لها. إنها ليست مثل لغة بايثون أو جافا النموذجية؛ إنها لغة تورينج كاملة مصممة خصيصًا لإثبات صحة البرامج قبل تشغيلها. تخيل أنك قادر على الوثوق بشكل كامل في تنفيذ البرنامج الخاص بك، حتى على جهاز لا تتحكم فيه بشكل كامل!

## إعداد بيئة التطوير

في حال لم تقوم في تثبيت بيئة التطوير الأساسية في جهازك, يمكنك العودة إلى الدرس السابق من اجل تثبيتها ومن ثم إكمال الدرس.

طريقة إعداد بيئة التطوير:
https://youtu.be/7YE2ZBszRBg

في هذا الدرس سوف نستخدم أداة **scarb** من أجل تشغيل وإختبار الكود الخاص بنا بكل سهولة

سنقوم بفتح **terminal** او **cmd** ومن ثم إنشاء مجلد يُدعى **cairo_lesson**

```bash
mkdir cairo_lesson & cd cairo_lesson
```

من أجل إنشاء بيئة **scarb** سنقوم بتشغيل هذا الأمر

```bash
scarb init
```

تم إنشاء البيئة بشكل جيد!

**الملفات الأساسية التي سنتعامل معها:**

- ملف **Scarb.toml** من أجل التعامل مع المشروع بالكامل.
- مجلد **src** هو المجلد الذي سنقوم بإنشاء الملفات الخاص بلغة cairo والتعامل معه - ستلاحظ ان هناك ملف تلقائي بإسم **lib.cairo** وهذا هو المجلد الذي سنقوم بالتعديل عليه طوال هذا الدرس.

من اجل تشغيل الكود او اختباره طوال هذا الدرس ستقوم بإدخال هذا الأمر:

```bash
scarb cairo-run --available-gas=200000000
```

ستلاحظ بعد تشغيل هذا الأمر قد تم إنشاء مجلد جديد يُدعى **target** ستحتاجه في الدروس القادمة أثناء نشر العقود الذكية على **starknet**. في هذا الدرس سنركز فقط في تعلم أساسيات لغة **cairo**.

لغة **Cairo** تشبه لغة **Rust** فلذلك تُعد فرصة جيدة لتعلم هذه اللغة لكون لغة Rust من أكثر اللغات المدفوعة في سوق العمل لقلة عدد المطورين وربما صعوبتها لكونها مختلفة قليلاً عن باقي لغات البرمجة.

### الشكل الأساسي للكود

للبدء في كتابة أكواد cairo سنقوم بتعريف دالة تُدعى **main** ومن ثم كتابة الأكواد في داخل الدالة من اجل ان يستطيع **scarb** من ترجمتها. سنقوم بشرح الدوال في الأسفل كل ما يهم معرفته هو الشكل العام:

```rust
fn main() {

}
```
يمكنك إكمال الدرس على اليوتيوب بكل سهولة:
https://youtu.be/8EcPUjcIuds


### الطباعة - Print

من المهم توضيح هذا في البداية! من أجل طباعة اي نص تريده ستقوم بإستخدام الأمر <span dir="ltr">**println!()**</span>.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة:

```rust
fn main() {
    println!("Hello World");

    println!("5");
    println!("{}", 5);

    println!("My name is AH and my age {}", 20);

    println!("The month = {} and the week = {}", 30, 7);
}
```

**دعونا نقوم بتوضيح كل سطر:**

- **السطر 2:** قمنا بطباعة Hello World مثل باقي لغات البرمجة الأخرى.
- **السطر 4 و 5:** على الرغم من أن الأمرين يقوموا بطباعة رقم 5 لكن الطريقة الثانية من المهم معرفتها سنحتاجها عندما نريد طباعة المتغيرات.
- **السطر 7 و 9:** بنفس فكرة السطر 5 ولكن امثلة إضافية لفهم طريقة استخدام الأقواس المتعرجة {}.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

## المتغيرات

**في لغة Cairo هناك 2 أنواع من المتغيرات وهي:**

1. متغيرات غير قابلة للتعديل تلقائياً ويتم تعريفها بإستخدام كلمة let ومن الممكن جعلها قابلة للتغيير بكل سهولة عن طريقة إضافة mut.
2. متغيرات غير قابلة للتعديل إطلاقاً ويتم تعريفها بإستخدام كلمة const.

سنفهم الان من خلال الكود التالي:
قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة

```rust
const ONE_HOUR_IN_SECONDS: u128 = 3600;

fn main () {
    let number_1: u128 = 10;
    println!("Number 1 = {}", number_1);

    let number_2: u256 = 15;
    println!("Number 2 = {}", number_2);

    let message: ByteArray = "Hello World!";
    println!("The message: {}", message);

    let boo: bool = true;
    println!("Boo is {}", boo);

    let mut nums: u128 = 5;
    println!("Before edit the variable: {}", nums);

    nums = 2;
    println!("After edit the variable: {}", nums);
    
    println!("{}", ONE_HOUR_IN_SECONDS);

    let num_1 = 100;
    let boos = true;
}
```

**دعونا نقوم بتوضيح كل سطر:**

- **السطر 1:** قمنا بتعريف متغير غير قابل للتعديل على الإطلاق بإستخدام **const** وإسم المتغير **ONE_HOUR_IN_SECONDS** وبما أن القيمة التي نريد تخزينها عددية موجبة اضفنا له نوع **u128** ومن ثم قمنا بإضافة القيمة وهي **3600** والتي تعبر قيمة الساعة بالثواني. (ملاحظة: المتغيرات الثابتة يتم تعريفها خارجة الدالة **main**). 
- **السطر 4:** قمنا بتعريف متغير عن طريق **let** (هذا النوع من المتغيرات في الأساس غير قابل لتعديل القيمة الخاص به ولكن من الممكن جعله قابل للتعديل سنرى ذلك في الأسطر القادمة) جعلنا إسم المتغير **number_1** وبما أن القيمة التي نريد تخزينها عددية موجبة اضفنا له نوع **u128** ومن ثم قمنا بإضافة القيمة وهي **10**. 
- **السطر 5:** قمنا بطباعة قيمة المتغير **number_1** وكما تلاحظ استخدمنا طريقة الأقواس المتعرجة **{}** في المكان الذي نريد طباعة القيمة **10** فيه.
- **السطر 7 و 8:** قمنا بتعريف متغير بإسم **number_2** ونوعه قيمة عددية موجبة ولكن التغيير الذي حدث في هذا المتغير هو حجم نوع المتغير وهي **u256** بدلاً من **u128** ومن ثم قمنا بإضافة القيمة **20** ومن ثم في السطر **8** قمنا بطباعة القيمة.
- **السطر 10 و 11:**  قمنا بتعريف متغير بإسم **message** وبما أن القيمة التي نريد تخزينها عبارة عن نص اضفنا له النوع **ByteArray** ومن ثم قمنا بتخزين النص الذي نريد تخزين وفي **السطر 11** قمنا بطباعة القيمة.
- **السطر 13 و 14:** قمنا بتعريف متغير بإسم **boo** وبما أن القيمة التي نريد تخزينها عبارة عن قيمة منطقية إما **true** أو **false** اضفنا له النوع **bool** ومن ثم قمنا بتخزين قيمة **true** وفي **السطر 14** قمنا بطباعة القيمة.
- **السطر 16 و 17:** قمنا بتعريف متغير بإسم **nums** ولكن ستلاحظ قبل إعطاء إسم للمتغير قمنا بإضافة كلمة **mut** وهذا يخبر المترجم بأن المتغير سيكون قابل للتعديل كما تحدثنا سابقاً ومن ثم بعد قمنا بتحديد النوع **u128** وإضافة القيمة **5** وفي **السطر 17** قمنا بطباعة المتغير وستلاحظ أن القيمة التي سيتم طباعتها هي **5**.
- **السطر 19 و 20:** بعد ان قمنا بتعريف المتغير **nums** والذي قمنا بتحديد المتغير كمتغير قابل للتعديل في **السطر 19** قمنا بتغيير قيمة المتغير من **5** إلى **2** وفي **السطر 20** قمنا بطباعة قيمة المتغير وستلاحظ أن القيمة التي سيتم طباعتها هي **2**.
- **السطر 22:** قمنا بطباعة قيمة المتغير الثابت الذي قمنا بتعريفه في السطر 1.
- **السطر 24 و 25:** قمنا بتعريف 2 متغيرات في السطرين ويقومون بنفس غرض المتغيرات في الأعلى ولكن هذه المرة لم نقوم بإعطاء نوع محدد للمتغير مسبقاً. ويُفضل دائماً إعطاء نوع للمتغير أثناء تعريفه.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

لمعرفة المزيد من أنواع المتغيرات يمكنك القفز إلى <a href="https://book.cairo-lang.org/ch02-02-data-types.html" target="_blank">وثائق Cairo من هنا</a>.

### أوامر الشرط - if/else

يتم استخدام عبارة if/else لتنفيذ كود مختلف اعتمادًا على شرط معين.

سنفهم الان من خلال الكود التالي: قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة

```rust
fn main() {
    let num: u8 = 5;

    if num > 10 {
        println!("big number");
    }
    else if num == 10 {
        println!("good number");
    }
    else {
        println!("bad number");
    }
}
```

**دعونا نقوم بتوضيح كل سطر:**

- **السطر 2:** قمنا بتعريف متغير بإسم **nums** بقيمة عددية وهي **10**.
- **السطر 4 - 6:** قمنا بإضافة شرط بإستخدام كلمة **if** وهو في حال كان قيمة المتغير"أكبر من" **10** سيقوم بطباعة "big number".
- **السطر 7 - 9:** قمنا بإضافة شرط آخر بإستخدام كلمة **else if** في حال لم يتحقق الشرط السابق وهو في حال كان قيمة المتغير"تساوي" **10** سيقوم بطباعة "good number". (يمكنك أيضاً إضافة شروط إضافية ولكننا سنكتفي بشرط إضافي واحد).
- **السطر 10 - 12:** قمنا بإضافة شرط بإستخدام كلمة **else** والتي تعني في حال لم يتحقق اي شرط من الشروط السابقة قم بطباعة "bad number".

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

### الدوال - Functions

يتم التعامل مع الدوال في لغة **Cairo** مثل العديد من لغات البرمجة. يمكننا إنشاء دوال لإعادة قيمة معينة أو لإجراء عمليات عديدة. دعونا ننتقل إلى الأمثلة مباشرة.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة

```rust
fn main() {
    let value = sum(10, 20);
    println!("The value: {}", value);

    check(8);
}

fn sum(x: u32, y: u32) -> u32 {
    x + y
}

fn check(val: u32) {
    if val >= 10 {
        println!("Big number");
    } else {
        println!("Small number");
    }
}
```

**في الكود السابق لدينا 3 دوال وهم:**

- **دالة main:** كما تحدثنا عنها سابقاً هي الدالة الاساسية لكي يعمل البرنامج ونقوم بتشغيل اي دالة اخرى نقوم بإنشائها داخل دالة **main**.
- **دالة sum:** قمنا بتعريف دالة تُدعى **sum** تقوم بإستقبال عددين وهو **x** و **y** لكي نقوم بجمع العددين وعندما نريد الدالة تقوم بإعادة قيمة معينة نقوم بإضافة <span dir="ltr">**-> u32**</span> في الدالة والتي تعني بأن القيمة التي سيتم إرجاعها أثناء تشغيل الدالة هي قيمة عددية (حاصل جمع العددين). كما تلاحظ قمنا باستدعاء دالة **sum** في دالة **main** في **السطر 2** وادخلنا لها العددين الذي نود جمعهما وقمنا بتخزين الناتج من الدالة (حاصل جمع العددين) في المتغير **value** وفي **السطر 3** قمنا بطباعة ما داخل المتغير.
- **دالة check:** قمنا بتعريف دالة تُدعى **check** تقوم بإستقبال قيمة عددية بإسم **val** وظيفة الدالة تقوم بإجراء عمليات معينة ولن تعيد أي قيمة مثل الدالة **sum**. كل ما ستقوم به هو التحقق في حال كانت قيمة **val** "اكبر من او يساوي" **10** يقوم بطباعة Big number وإن لم يتحقق الشرط يقوم بطباعة Small number. ومن ثم قمنا بتشغيل الدالة check عن طريق استدعائها في الدالة **main** في **السطر 5** وادخلنا لها قيمة وهي **8**.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

يمكننا الحصول على المزيد من الأمثلة <a href="https://book.cairo-lang.org/ch02-03-functions.html" target="_blank">من هنا</a>. ولكن لا تقلق سنذكر العديد من الأمثلة في الأوقات القادمة وأيضاً في الدروس القادمة أثناء كتابة العقود الذكية. فقط استمر في التعلم.

### المصفوفات - Arrays

تعمل المصفوفات في Cairo بنفس الطريقة التي تعمل بها في لغات البرمجة الأخرى. دعونا ننتقل إلى الأمثلة مباشرة.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح أعلى كل سطر:

```rust
fn main() {
    // تعريف متغير قابل للتعديل يقوم بتخزين مصفوفة جديدة
    let mut arr = ArrayTrait::new();

    // إضافة أربعة قيم للمصفوفة
    arr.append(5);
    arr.append(10);
    arr.append(15);
    arr.append('hi');

    // في المصفوفات يبدأ موقع القيم التي ندخلها من الرقم 0
    // طباعة القيمة الأولى التي موقعها رقم 0
    println!("Index 0: {}", *arr.at(0));
    // طباعة القيمة الثانية التي موقعها رقم 1
    println!("Index 1: {}", *arr.at(1));

    // طباعة حجم المصفوفة
    println!("The len: {}", arr.len());

    // إزالة اول عنصر في المصفوفة
    arr.pop_front().unwrap();
    // إزالة اول عنصر في المصفوفة
    arr.pop_front().unwrap();

    // طباعة القيمة الأولى التي موقعها رقم 0
    println!("Index 0: {}", *arr.at(0));

    // طباعة حجم المصفوفة
    println!("The len: {}", arr.len());
}
```

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

### الهياكل - Structs

الهياكل في **Cairo** هي طريقة لتعريف الأنواع المخصصة مع أعضاء من الأنواع الأخرى. إنها مفيدة لتجميع البيانات ذات الصلة معًا، مثل عناوين الكتب والمؤلفين وأرقام ISBN في مكتبة. يمكن استخدام الهياكل لتخزين أنواع البيانات المعقدة مثل mappings والمصفوفات. بالإضافة إلى ذلك، يمكن تخزين الهياكل في هياكل أخرى، مما يسمح بتداخل البيانات.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح أعلى كل سطر:

```rust
// تقوم هذه بالسماح للهيكل في إستدعائه بداخل الدوال او نسخه
#[derive(Drop, Copy)]
// قم بتعريف الهيكل الخاص بالموظفين الذي يجمع بين ثلاثة أنواع من البيانات
struct Employee {
    name: felt252,
    age: u32,
    salary: u32,
}

fn main() {
    // نقوم بتخزين بيانات الموظف في المتغير حسب الأنواع التي حددناها في الهيكل
    let employee: Employee = Employee { name: 'ali', age: 20, salary: 5000 };

    // طباعة إسم الموظف
    println!("{}", employee.name);
    // طباعة عمر الموظف
    println!("{}", employee.age);
    // طباعة راتب الموظف
    println!("{}", employee.salary);
}
```

كما تلاحظ في الأعلى عندما قمنا بتعريف المتغير employee قمنا بجعل نوعه حسب الهيكل Employee بحيث يستقبل جميع أنواع البيانات التي نود تخزينها دون مشاكل.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

### التعامل مع الهياكل والدوال

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح أعلى كل سطر:

```rust
// تقوم هذه بالسماح للهيكل في إستدعائه بداخل الدوال او نسخه
#[derive(Drop, Copy)]
// قم بتعريف الهيكل الخاص بالاشخاص الذي يجمع بين اربعة أنواع من البيانات
struct Person {
    name: felt252,
    email: felt252,
    age: u32,
    year_join: u32, 
}

fn main() {
    // نقوم بتخزين بيانات الشخص في المتغير حسب الأنواع التي حددناها في الهيكل
    let per: Person = Person { name: "Ali", email: "ali@gmail.com", age: 20, year_join: 2023 };

    // إليها per إستدعاء الدالة وإدخال بيانات المتغير
    print_person(per);
    
    // year_birthday إنشاء متغير يقوم تخزين السنة من الدالة
    let year: u32 = year_birthday(per);
    // طباعة سنة ميلاد الشخص
    println!("The year birthday: {}", year);
}

// تقوم بطباعة جميع بيانات الشخص Person بإستقبال قيمة نوعها الهيكل print_person تقوم الدالة 
fn print_person(val: Person) {
    println!("name: {}", val.name);
    println!("email: {}", val.email);
    println!("age: {}", val.age);
    println!("year_join: {}", val.year_join);
}

// Person بإستقبال قيمة نوعها الهيكل year_birthday تقوم الدالة
// وظيفة الدالة إرجاع قيمة عددية وهي ناتج سنة إنضمام الشخص طرح عمره
fn year_birthday(val: Person) -> u32 {
    val.year_join - val.age
}
```

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

### Trait & Impl

كما تلاحظ في المثال السابق أثناء التعامل مع الدوال يبدو الأمر مرهق قليلاً في حال كان المشروع كبير وتريد استخدام بشكل أكبر في العديد من الملفات.

ولكن بإستخدام Trait و Impl يمكننا تنظيم المشروع بشكل بسيط كواجهات والتعامل مع structs بشكل بسيط.

بواسطة **Trait** نقوم بتجميع الدوال في مكان واحد كمجموعة ومن ثم استخدامها في **Impl** كواجهة بحيث نكمل البناء على اساس هذه الواجهة.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة:

```rust
#[derive(Drop, Copy)]
struct Person {
    name: felt252,
    email: felt252,
    age: u32,
    year_join: u32, 
}

trait IPerson {
    fn year_birthday(self: Person) -> u32;
    fn edit_year_join(ref self: Person, newYear: u32);
}

impl PersonImpl of IPerson {
    fn year_birthday(self: Person) -> u32 {
        self.year_join - self.age
    }

    fn edit_year_join(ref self: Person, newYear: u32) {
        self.year_join = newYear;
    }
}

fn main() {
    let mut per = Person { name: "Ali", email: "ali@gmail.com", age: 20, year_join: 2020 };

    println!("Year join: {}", per.year_join);

    let year: u32 = per.year_birthday();
    println!("The year birthday: {}", year);

    per.edit_year_join(2024);
    println!("Year join: {}", per.year_join);
}
```

**دعونا نقوم بتوضيح كل سطر:**

- **السطر 1 - 7:** قمنا بإنشاء **struct** يُدعئ **Person** من أجل إنشاء هيكل البيانات التي نريد تخزينها مثل الاسم والايميل والعمر وسنة الإنضمام.
- **السطر 9 - 12:** قمنا بإنشاء **trait** (أو واجهة) بإسم **IPerson** والإعلان عن دالتين تقوم الأولى بجلب سنة الميلاد والثانية التعديل على سنة الانضمام. ولكن كما تلاحظ انها مجرد واجهات لا تقوم بتشغيل شيء.
- **السطر 14 - 22:** قمنا بإنشاء **impl** بإسم **PersonImpl** يقوم بإستخدام trait (واجهة) **IPerson**. وكما تلاحظ ستقوم بداخل **impl** بناء الدوال التي قمت بالإعلان عنها في **trait** فقط. في **السطر 15** قمنا بكتابة الدالة **year_birthday** وقمنا بتمرير **self** يقوم بنسخ **struct Person** والذي من خلاله سنقوم بالوصول الى المتغيرات التي في داخل الهيكل ومن ثم في داخل الدالة قمنا بتشغيل عملية حسابية وهي سنة الإنضمام طرح العمل بحيث يقوم بإرجاع قيمة عددية وهي سنة الميلاد. وفي **السطر 19** قمنا بكتابة الدالة **edit_year_join** والتي تقوم بتعديل سنة الإنضمام ولكن كما تلاحظ أثناء تمرير المتغير **self** لنسخ الهيكل **Person** قمنا بإضافة **ref** قبل المتغير **self** والذي يسمح لنا بالتعديل على البيانات بشكل طبيعي وقمنا ايضا بتمرير متغير **newYear** وهي القيمة الجديدة التي نريد تخزينها ومن ثم قمنا بإضافة قيمة **newYear** في سنة الانضمام.
- **السطر 24 - 34:** قمنا بتضمين كل ما قمنا ببنائه في الدالة الرئيسية **main** بحيث قمنا بتخزين بيانات الهيكل في المتغير **per** وبعد ذلك قمنا بتشغيل الدوال التي في **impl** عن طريق المتغير **per** بكل سهولة.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

قد يبدو الأمر بالنسبة لك غريباً ولكن أثناء بناء العقود الذكية والاستمرار في البناء سيصبح الامر اكثر سهولة.

### الوحدات - Modules

تساعد الوحدات في **Cairo** في تقسيم البرنامج إلى وحدات منطقية لتحسين إمكانية القراءة والتنظيم. يمكننا التعبير مثل **oop** في لغات البرمجة الشائعة.

بمجرد أن يصبح البرنامج أكبر، من المهم تقسيمه إلى ملفات أو مساحات أسماء متعددة. تساعد الوحدات (Modules) في هيكلة برنامجنا وتنظيمه.

قد يحتوي modules الى مجموعة من العناصر مثل: الدوال - Functions والهياكل - Structs وحتى وحدات modules إضافية في الداخل.

قم بنسخ الكود إلى الملف **lib.cairo** ومن ثم قُم بمتابعة الشرح اسفل الكود مباشرة:

```rust
mod config {
    pub fn prints() {
        println!("Hello world!");
    }

    pub fn sum(x: u8, y: u8) -> u8 {
        x + y
    }
}

fn main() {
    config::prints();

    let result = config::sum(5, 10);
    println!("{}", result);
}
```

**دعونا نقوم بتوضيح كل سطر:**

- **السطر 1 - 9:** قمنا بتعريف وحدة بإستخدام الأمر **mod** ومن ثم قمنا بإعطاء إسم لها وهو **config**. كما تحدثنا سابقاً فإن الوحدات من الممكن أن تحتوي على دوال وهياكل ووحدات ايضاً فقمنا في المثال الذي في الأعلى بإضافة دالتين الدالة الأولى تُدعى **prints** وتقوم بطباعة نص والدالة الثانية تُدعئ **sum** تقوم بإرجاع حاصل جمع عددين.
- **السطر 11 - 16:** من اجل ان يتمكن المترجم من قراءة الملف قمنا بإنشاء الدالة الرئيسية **main** وفي **السطر 12** قمنا باستدعاء الدالة **prints** من الوحدة config عن طريق <span dir="ltr">**config::prints()**</span>. وفي **السطر 14** قمنا باستدعاء الدالة **sum** من الوحدة **config** وقمنا بإدخال رقمين وتخزين الناتج في المتغير **sum1** وفي **السطر 15** قمنا بطباعة قيمة المتغير **sum1**.

قم بتجربة وتطبيق الكود الذي في الأعلى لرؤية النتائج في جهازك.

لا تقلق في حال لم تستطيع فهمها بسرعة; سنقوم بإستخدام **mod** بشكل أساسي في الدرس القادم أثناء إنشاء عقود ذكية.

يمكنك حل بعض المشاكل التي قمنا بحلها في الحلقة الثالثة من المعسكر التدريبي من هنا:
https://youtu.be/Vl_1vobuGd4

كما هو الحال دائمًا، إذا كانت لديك أي أسئلة أو شعرت بالتعثر أو أردت فقط أن تقول مرحبًا، فقم بالإنضمام على <a href="https://t.me/Web3ArabsDAO" target="_blank">Telegram</a> او <a href="https://discord.gg/ykgUvqMc4Q" target="_blank">Discord</a> وسنكون أكثر من سعداء لمساعدتك!
