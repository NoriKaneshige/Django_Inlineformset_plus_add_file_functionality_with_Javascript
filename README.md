# Django_Inlineformset_plus_add_file_functionality_with_Javascript

[referred blog](https://narito.ninja/blog/detail/36/)

![inlineformset-plus-add-file-func](inlineformset-plus-add-file-func.gif)

> ## post_form.html
> ## Adding element by Javascript. Everything else is the same as inlineformset
``` python
{% extends 'app/base.html' %}

{% block content %}
<!-- Because we use file, we need enctype="multipart/form-data" -->
<form action="" method="post" enctype="multipart/form-data">
    <h2>Post</h2>
    {{ form.as_p }}

    <h2>attach file</h2>
    {{ formset.management_form }}

    <div id="file-area">
        {% for file_form in formset %}
            {{ file_form.as_p }}
            <hr>
        {% endfor %}
    </div>
    
    {% csrf_token %}
    <button type="submit" class="btn btn-primary">Submit</button>
    <button id="add" type="button" class="btn btn-primary">ファイルの追加</button>
</form>
{% endblock %}

{% block extrajs %}
<script>
$(function(){
    var totalManageElement = $('input#id_file_set-TOTAL_FORMS');
    var currentFileCount = parseInt(totalManageElement.val());
    $('button#add').on('click', function(){
        var nameElement = $('<input>', {
            type: 'name',
            name: 'file_set-' + currentFileCount + '-name',
            id: 'id_file_set-' + currentFileCount + '-name',
        });
        var fileElement = $('<input>', {
            type: 'file',
            name: 'file_set-' + currentFileCount + '-src',
            id: 'id_file_set-' + currentFileCount + '-src',
        });
        $('div#file-area').append(nameElement);
        $('div#file-area').append(fileElement);
        currentFileCount += 1;
        totalManageElement.attr('value', currentFileCount);
    });
});
</script>
{% endblock %}
```
