<script setup>

</script>

<template>
    <div class="card">
        <h1>Busque por um perfil</h1>
        <input type="text" placeholder="Digite o nome de usuário" />
    </div>
    <div class="card">
        <h1 class="login title">Lucas Bello</h1>
        <h4 class="username">belloLucas</h4>
        <h4 class="location">Juiz de Fora</h4>
        <h4 class="bio">Desenvolvedor Front-end</h4>
        <div class="followers">
            <h5 class="followers">15</h5>
            <h5 class="following">24</h5>
        </div>
    </div>
</template>

<style scoped lang="scss">
    .card {
        padding: 20px;
        border-radius: 5px;
        text-align: center;
        background-color: #f4f4f4;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

        input {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
    }
</style>