<script>
    const student = {name: 'Rico Weigel'};
    const myList = ['Birdo', 'Mario Kart', 'The Hunger Games', 'Lost'];
</script>

My name is {student.name} and these are some of my favourite things: 

{#each myList as item}
    <li>{item}</li>
{/each}