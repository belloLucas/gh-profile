<template>
    <div class="card">
        <div class="search-input">
            <h1>Busque por um perfil</h1>
            <div class="inputs">
                <input type="text" placeholder="Digite o nome de usuário" v-model="username"/>
                <button type="submit" @click="fetchData(username)" >Pesquisar</button>
            </div>
        </div>

        <div class="profile-card" v-if="login">
            <img class="profile-img" :src="avatar_url" alt="Lucas Bello" />
            <h1 class="name title">{{ name }}</h1>
            <h4 class="username">@{{ login }}</h4>
            <h4 class="bio">{{ bio }}</h4>
            

            <div class="followers">
                <h5 class="followers"> {{ followers }} <span>seguidores</span></h5>
                <h5 class="following">{{ following }} <span>seguindo</span></h5>
            </div>

            <div class="socials">
                <h5 class="social">Twitter: @{{ twitter_username }}</h5>
                <h5 class="social">Site: {{ blog }}</h5>
            </div>

            <div class="repos">
                <h5 class="repo">Repositórios Públicos: {{ public_repos }}</h5>
            </div>

            <h4 class="location">📍 {{ location }}</h4>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            username: '',
            bio: '',
            location: '',
            followers: '',
            following: '',
            public_repos: '',
            twitter_username: '',
            blog: '',
            avatar_url: '',
            email: '',
            name: '',
            login: '',
        }
    },
    methods: {
        async fetchData(username) {
            try{
                if(!username) {
                    throw new Error('Usuário não encontrado');
                }

                const response = await fetch(`https://api.github.com/users/${this.username}`);
                const data = await response.json();

                data.bio ? this.bio = data.bio : this.bio = 'Sem bio';
                data.location ? this.location = data.location : this.location = 'Sem localização';
                data.followers ? this.followers = data.followers : this.followers = 'Sem seguidores';
                data.following ? this.following = data.following : this.following = 'Sem seguindo';
                data.public_repos ? this.public_repos = data.public_repos : this.public_repos = 'Sem repositórios públicos';
                data.twitter_username ? this.twitter_username = data.twitter_username : this.twitter_username = 'Sem twitter';
                data.blog ? this.blog = data.blog : this.blog = 'Sem blog';
                data.avatar_url ? this.avatar_url = data.avatar_url : this.avatar_url = 'Sem imagem';
                data.email ? this.email = data.email : this.email = 'Sem email';
                data.name ? this.name = data.name : this.name = 'Sem nome';
                data.login ? this.login = data.login : this.login = 'Sem login';
            } catch (error) {
                throw new Error(error)
            }

        }
    }
}
</script>

<style scoped lang="scss">
    .card {
        width: 30%;
        padding: 20px;
        border-radius: 5px;
        text-align: center;
        background-color: #f4f4f4;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

        .search-input {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            border-bottom: 1px solid #ccc;

            .inputs {
                display: flex;
                margin-top: 20px;

                form {
                    width: 100%;
                }

                input {
                    width: 70%;
                    padding: 10px;
                    border: 1px solid #ccc;
                    border-top-left-radius: 5px;
                    border-bottom-left-radius: 5px;
                    outline: none;
                }
                button {
                    width: 30%;
                    padding: 10px;
                    border: none;
                    border-top-right-radius: 5px;
                    border-bottom-right-radius: 5px;
                    background-color: #333;
                    color: #fff;
                    cursor: pointer;
                    outline: none;

                    :hover {
                        background-color: #555;
                    }
                }
            }

        }

        .profile-card {
            display: flex;
            flex-direction: column;
            gap: 10px;
            padding: 20px;
            margin-top: 20px;
            border-radius: 5px;
            background-color: #fff;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);

            .profile-img {
                width: 120px;
                height: 120px;
                border-radius: 5px;
                margin: 0 auto;
            }

            .title {
                font-size: 24px;
            }

            .username {
                font-size: 16px;
                color: #666;
            }

            .location {
                font-size: 16px;
                color: #666;
            }

            .bio {
                border: 1px solid #ccc;
                border-radius: 5px;
                padding: 5px;
                font-size: 16px;
                color: #666;
            }

            .followers {
                display: flex;
                justify-content: space-around;

                h5 {
                    display: flex;
                    align-items: center;
                    gap: 5px;
                    margin: 0;
                    font-size: 18px;
                    color: #666;

                    span {
                        font-size: 16px;
                        color: #999;
                    }
                }
            }

            .repos {
                margin: 10px 0;
                font-size: 18px;
                color: #666;
            }

            .socials {
                display: flex;
                align-items: center;
                justify-content: space-around;

                h5 {
                    gap: 5px;
                    margin: 0;
                    font-size: 16px;
                    color: #666;
                }
            }
        }
    }
</style>