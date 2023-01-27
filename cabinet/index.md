---
  layout: default
  title: Cabinet Members
---

<div class="table-responsive">
<table class="table">
  <tr>
  <th style="width: 30%">Position</th>
  <th style="width: 30%">Name(s)</th>
  <th style="width: 40%">Email(s)</th>
  </tr>
{% for office in site.data.cabinet.cabinet.cabinet %}
  {% for member in office.officers %}
  <tr>
  {% if forloop.first == true %}
  <td rowspan={{ forloop.length }}>
  {{ office.position }}
  </td>
  {% endif %}
  
  <td>{{ member.name }}</td>
  <td>{{ member.email | replace: "@", " [at] "}}</td>
  </tr>
  {% else %}
  <tr>
  <td>
  {{ office.position }}
  </td>
  <td colspan="2" style="text-align: center;">
  <i>This position is currently vacant, contact the president for any relavant matters.</i> 
  </td>
  </tr>
  {% endfor %}
{% endfor %}
</table>
</div>
