---
layout: post
title: Flexbox - מדריך למתחילים - חלק ב׳
excerpt: החלק השני במדריך פלקסבוקס, בו נעסוק במאפיינים אשר מחילים על ה- Flex Items.
thumbnail: http://devhead.co.il/images/thumbnails/flexbox-part-2.png
---

כמו שראינו בחלק הראשון של המדריך, פלקסבוקס יכול לעזור לנו ב״פריסת״ העיצוב שלנו. ניתן לקבוע את הכיוון בו אלמנטים יפרסו ואם הם ידחסו בשורה אחת או יגלשו לשורות חדשות בהתאם לגודלן, וכן להגדיר את היישור האנכי והאופקי של האלמנטים.

אבל מה אם נרצה לשלוט בגודל האלמנטים שלנו?  
אם נרצה למשל, לשנות גודל אלמנט כך שיהיה גדול פי 3 מהאלמנט הסמוך אליו, כאשר יש מספיק מקום לשניהם בשורה, ואם לא - שכל אחד מהם יתפוס שורה שלמה.

אפשר לבצע זאת כמובן גם ללא פלקסבוקס, אך מיד נראה איך הוא הופך את כל התהליך להרבה יותר פשוט ומהיר.

### `flex`

זהו כנראה המאפיין שתמצאו הכי “מהפכני” בין כל המאפיינים, ואולי בגלל זה הוא יכול לבלבל כל כך. אני חייב להודות שרק לאחרונה התחלתי להבין איך הוא עובד בדיוק.  
`flex` מוגדר על ה- Flex Items ומאפשר להם לגדול או להתכווץ ביחס למקום שנשאר בציר הראשי. ככה הוא נראה:

{% highlight css %}
.item {
  flex: 1 1 150px;
}
{% endhighlight %}

flex הוא קיצור של שלושה מאפיינים.

* הראשון נקרא **`flex-grow`**, והוא קובע מה היחס בו האלמנט יגדל בהשוואה לשאר האלמנטים, במידה ויש מקום פנוי בשורה בה הוא נמצא.  
ברירת המחדל שלו היא 0 - האלמנט לא יגדל גם אם יש מקום בשורה.  
בדוגמה קבענו שהערך שלו יהיה 1, כך שהאלמנט יקבל חלק אחד מכל פיקסל פנוי בשורה.  

* השני נקרא **`flex-shrink`**, והוא עושה ההפך מהמאפיין הקודם - קובע בכמה האלמנט יתכווץ בהשוואה לשאר האלמנטים, במידה ואין מקום פנוי בשורה בה הוא נמצא והאלמנטים מתחילים ל”גלוש” מחוץ אליה.  
בדוגמה קבענו שהערך שלו יהיה 1 (זוהי גם ברירת המחדל), כך שגודל האלמנט יקטן בחלק אחד מכל פיקסל ״גולש״ בשורה, כאשר אין בה מספיק מקום.  

* השלישי נקרא **`flex-basis`**, והוא קובע את הגודל ההתחלתי של האלמנט לפני שהוא מתחיל לגדול / להתכווץ בעזרת שני המאפיינים הקודמים.  
ברירת המחדל שלו היא auto - גודל האלמנט ייקבע לפי ה[גודל הראשי](/flexbox-part-1#main-size) שלו.  
בדוגמה קבענו שהערך שלו יהיה 150px, כך שבמידה והגודל הראשי של האלמנט הוא הרוחב, זה יהיה הרוחב ההתחלתי שלו.

שני המאפיינים הראשונים מקבלים מספר חיובי ושלם שיקבע את היחס הפרופורציונלי, בעוד השלישי מקבל את אותם הערכים שהמאפיין `width`, למשל, יכול לקבל - px, em, אחוזים וכו׳.

אם לא התפוצץ לכם הראש מהפסקאות האחרונות אתם יכולים להיות גאים בעצמכם. אם כן - אתם בסדר גמור. `flex` הוא המאפיין שהכי קשה לתפוס ולהבין איך הוא עובד מבין המאפיינים של פלקסבוקס, ואני מקווה שהדוגמה הבאה תבהיר במעט את השימוש בו.

<p data-height="268" data-theme-id="0" data-slug-hash="wMyEgo" data-default-tab="result" data-user="guytepper" class='codepen'>See the Pen <a href='http://codepen.io/guytepper/pen/wMyEgo/'>flex Property Demo #1</a> by Guy (<a href='http://codepen.io/guytepper'>@guytepper</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

**אז מה קורה כאן?**

נתחיל מהקונטיינר. לא שינינו את `flex-direction`, כך שהציר הראשי שלנו הוא מימין לשמאל. בנוסף, אפשרנו את `flex-wrap`, כך שהילדים שלנו יכולים לגלוש לשורות חדשות במידה ואין מספיק מקום להכיל את כל הילדים באותה השורה.  
פתחו את הדמו ב- CodePen, שנו את גודל החלון ושימו לב מה קורה 😎

כאשר נפעיל את הקוד שראינו מקודם, הדבר הראשון שיקרה הוא שהערך שציינו ב-`flex-basis` יוחל על כל אחד מהילדים. כלומר, הרוחב (שהוא הגודל הראשי) ההתחלתי של כל הילדים יהיה 150px.

לאחר מכן הדפדפן יבדוק לגבי כל ילד כמה מקום פנוי יש בשורה בה הוא נמצא. כאשר יש מקום פנוי, כל פיקסל ממנו יחולק בצורה שוויונית בין כל אחד מהילדים באותה השורה, ובכך יגדיל את הגודל הראשי שלהם. כאשר אין מקום פנוי בשורה, כל אחד מהילדים באותה השורה יוריד מהגודל הראשי שלו כמות שווה של פיקסלים. הגודל ממנו מורידים / מוסיפים פיקסלים, הוא ה-`flex-basis`.  

כמובן שאם נשנה את הערך של `flex-grow` או `flex-shrink` ספציפית לאחד האלמנטים, חלוקת הפיקסלים לא תהיה שווה. בדוגמה הבאה תוכלו לראות זאת בא לידי ביטוי.

### סדר חדש

בעולם הרספונסיבי של היום לא תמיד נרצה להציג את העיצוב שלנו באותו סדר כמו שהוא מופיע בקוד המקור שלנו. ייתכן שנרצה, כמו שנראה בדוגמה הבאה, להציג את תפריט הניווט לפני התוכן ברזולוציות גבוהות, אך ברזולוציות נמוכות להעביר את התפריט לתחתית העמוד.

בעזרת המאפיין `order` נוכל לשלוט בסדר ה- Flex Items באופן דינמי. המאפיין מקבל מספר שלם שיקבע את המיקום בו הוא יופיע.

{% highlight css %}
.item {
  order: 2;
}
{% endhighlight %}

שימו לב ש- `order` קובע את המיקום הויזואלי בלבד, ולא משנה את מיקום האלמנטים בקוד המקור.

### Holy Grail Layout

בדוגמה הבאה נראה איך אפשר להשתמש בפלקסבוקס ובמאפיינים האחרונים שלמדנו על מנת ליצור את ה- *Holy Grail Layout*, העיצוב הסטנדרטי של אתרי אינטרנט שמורכב מלוגו, תפריט ניווט, תוכן, סיידבר ופוטר.

<p data-height="306" data-theme-id="0" data-slug-hash="QyzEpK" data-default-tab="result" data-user="guytepper" class='codepen'>See the Pen <a href='http://codepen.io/guytepper/pen/QyzEpK/'>Holy Grail Layout with Flexbox </a> by Guy (<a href='http://codepen.io/guytepper'>@guytepper</a>) on <a href='http://codepen.io'>CodePen</a>.</p>
<script async src="//assets.codepen.io/assets/embed/ei.js"></script>

הבעיה העיקרית שהייתה עד כה עם העיצוב הזה היא שלא היה פשוט להגיע למצב שהעמודות האמצעיות (ניווט, תוכן וסיידבר) יהיו בגבהים שווים.

בעיה זו נפתרה ברגע שהפעלנו את פלקסבוקס: `align-items` מוגדר כברירת מחדל ל-`stretch`, ככה שהגודל המשני של האלמנטים באותה השורה (גובה במקרה הזה) יהפוך להיות זהה ויקבע ע״י האלמנט הכי גדול.

אבל כאן לא הסתיימו הבעיות - כפי שתוכלו לראות, תפריט הניווט מופיע שני בקוד המקור. זה אחלה ברזולוציות גבוהות, אבל לא נרצה שזה הדבר הראשון שמשתמשי מובייל יראו כשייכנסו לאתר - נעדיף להראות להם את התוכן ראשון ובסוף העמוד את התפריט.

לכן הכנסתי את הברייקפוינט הבא:

{% highlight css %}

@media (max-width: 635px) {
  .nav {
    flex-basis: 100%;
    order: 2;
  }

  .footer {
    order: 3;
  }
}

{% endhighlight %}

כאשר משתמש עם מסך ברזולוציה נמוכה יכנס לאתר, הוא יראה את תפריט הניווט בתחתית הדף, במקום במיקום המקורי שלו בקוד המקור.  
בנוסף לכך שיניתי את ה- `flex-basis` כך שהאלמנט ייפרס על גבי כל השורה בה הוא נמצא.

מפני שערך ברירת המחדל של order הוא 0, יש צורך להגדיר אותו גם על ה- footer אם נרצה שישמור על מיקומו הויזואלי.



### `align-self`
רגע לפני שנסיים, יש עוד מאפיין אחד שצריך להזכיר.  
 `align-self` מוגדר על Flex Item ועושה את אותה הפעולה ש- [`align-items`](/flexbox-part-1#align-items) מבצע (ומקבל את אותם הערכים).  

בניגוד ל- `align-items`, המאפיין עובד על אלמנט ספציפי ולא על כל האלמנטים שתחת הקונטיינר.

---

זה הכל לבנתיים. אפשר לדבר עוד הרבה על פלקסבוקס והשימושים שלו בפועל, אבל זה כבר לפעם אחרת. שיהיה בהצלחה!

### קריאה נוספת
* [Flexbox Froggy](http://flexboxfroggy.com/) - לימדו על פלקסבוקס בעזרת משחק מגניב.
* [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) - מדריך נהדר מ- CSS-Tricks. שימושי בעת צרה.
* [מדריך באינטרנט ישראל](https://internet-israel.com/%D7%9E%D7%93%D7%A8%D7%99%D7%9B%D7%99%D7%9D/css3/css-flexbox-%D7%90%D7%9C%D7%9E%D7%A0%D7%98-%D7%90%D7%91/) - אם לא הספיקה לכם החפירה שלי, מוזמנים לנסות גם את המדריך של רן בר-זיק בנושא (-: