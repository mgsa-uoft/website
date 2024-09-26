---
  layout: default
  title: Members of the MGSA 
---

{% for committee_roles in site.data.cabinet.cabinet.committees %}
    {% assign committee = committee_roles[0] %}
    {% assign roles = committee_roles[1] %}
<h3>{{ committee | replace: '_', ' ' | capitalize }}</h3>

<div class="table-responsive">
<table class="table">
  <tr>
  <th style="width: 30%">Position</th>
  <th style="width: 30%">Name(s)</th>
  <th style="width: 40%">Email(s)</th>
  </tr>
{% for role in roles %}
  {% assign members = role.officers | sort : "name" %}
  {% for member in members %}
  <tr>
  {% if forloop.first == true %}
  <td rowspan={{ forloop.length }}>
  {{ role.position }}
  </td>
  {% endif %}
  
  <td>{{ member.name }}</td>
  <td>{{ member.email | replace: "@", " [at] "}}</td>
  </tr>
  {% else %}
  <tr>
  <td>
  {{ role.position }}
  </td>
  <td colspan="2" style="text-align: center;">
  <i>This position is currently vacant, contact the president for any relavant matters.</i> 
  </td>
  </tr>
  {% endfor %}
{% endfor %}
</table>
</div>

{% endfor %}
