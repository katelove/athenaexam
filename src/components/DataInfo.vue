<template>
  <tr>
    <th class="tableIcon">
      <div><font-awesome-icon icon="edit" @click="update()" /></div>
      <div><font-awesome-icon icon="trash-alt" @click="del()" /></div>
    </th>
    <td>{{ name }}</td>
    <td>{{ email }}</td>
    <td>{{ english }}</td>
    <td>{{ math }}</td>
    <td></td>
    <td></td>
  </tr>
</template>

<script>
export default {
  name: 'DataInfo',
  props: ['name', 'email', 'english', 'math']
}
</script>
