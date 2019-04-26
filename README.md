<div align="center">
    <img src="https://github.com/maikealame/laravel-auto/raw/master/docs/images/logo-tp.png" height="128">
    <a href="https://maikealame.github.io/laravel-auto/">
        <h1>LaravelAuto</h1>
    </a>
</div>

Laravel helper package to make automated lists with filters, sorting and paging like no other. 

Wiki: [https://maikealame.github.io/laravel-auto/](https://maikealame.github.io/laravel-auto/)

[![Latest Version](https://img.shields.io/github/release/maikealame/laravel-auto.svg?style=flat-square)](https://github.com/maikealame/laravel-auto/releases)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Total Downloads](https://img.shields.io/packagist/dt/maikealame/laravel-auto.svg?style=flat-square)](https://packagist.org/packages/maikealame/laravel-auto)


You are free to create your own layout and style, there's no layout html/css included !
This package only grants a very automated query in Eloquent with Blade directives.

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/1.png)

---

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/2.png)

---

```
$categories = Topic::from(Topic::table(true)." as t")
            ->select("t.*")
            ->leftJoin(Portal::table(true)." as p", "p.id","=","t.portal_id")
            ->autoWhere()->autoSort()->autoPaginate();
```

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/3.png)

---

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/4.png)

---

```
$notifications = Notification::select(Notification::table(true).".*", "notification_users.readed_at")
            ->groupBy("notifications.id")
            ->leftJoin(NotificationUser::table(true), "notifications.id", "=", "notification_users.notification_id")
            ->leftJoin(NotificationRole::table(true), "notifications.id", "=", "notification_users.notification_id")
            ->leftJoin(NotificationDepartment::table(true), "notifications.id", "=", "notification_users.notification_id")
            ->autoWhere(['or' => ["notifications.title", "notifications.description"]])
            ->autoSort(["notifications.updated_at", "desc"])->autoPaginate();
```

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/5.png)

---

```
if (Request::has("filter")) {
            if (isset(Request::get("filter")['keyword'])) {
                $keyword = Request::get("filter")['keyword'];
                Auto::setField("notifications.title", $keyword);
                Auto::setField("notifications.description", $keyword);

            }
}
$enterprises = Enterprises::from(Enterprises::table(true, "e"))
            ->select("e.*")
            ->leftJoin(EnterprisesIndicatorsEnterprises::table(true, "eie"),"eie.enterprise_id","=","e.id")
            ->groupBy("e.id")
            ->autoWhere()->autoSort()->autoPaginate();
```

![table image](https://raw.githubusercontent.com/maikealame/laravel-auto/master/docs/images/examples/6.png)

---

See https://maikealame.github.io/laravel-auto/

---

- [Features](https://maikealame.github.io/laravel-auto#features)
- [What it do](https://maikealame.github.io/laravel-auto#what-it-do)
- [What is necessary](https://maikealame.github.io/laravel-auto#what-is-necessary)
- [Wiki](https://maikealame.github.io/laravel-auto#wiki)
- [Examples](https://maikealame.github.io/laravel-auto#example)
- [How works](https://maikealame.github.io/laravel-auto#how-works)
1. [View](https://maikealame.github.io/laravel-auto#view)
2. [Controller](https://maikealame.github.io/laravel-auto#controller)
3. [Model](https://maikealame.github.io/laravel-auto#model)
- [How to install](https://maikealame.github.io/laravel-auto#how-to-install)
