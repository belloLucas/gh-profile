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
                if (!username) {
                    throw new Error('Nome de usuário precisa ser preenchido');
                }

                const response = await fetch(`https://api.github.com/users/${this.username}`);
                const data = await response.json();

                if (!data) {
                    throw new Error('Ocorreu um erro. Tente novamente.');
                }
                
                if (data.message === 'Not Found') {
                    throw new Error('Usuário não encontrado');
                } else {
                    this.bio = data.bio;
                    this.location = data.location;
                    this.followers = data.followers;
                    this.following = data.following;
                    this.public_repos = data.public_repos;
                    this.twitter_username = data.twitter_username;
                    this.blog = data.blog;
                    this.avatar_url = data.avatar_url;
                    this.email = data.email;
                    this.name = data.name;
                    this.login = data.login;
                }
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

        @media (max-width: 1100px) {
            width: 50%;
        }

        @media (max-width: 768px) {
            width: 60%;
        }

        @media (max-width: 560px) {
            width: 70%;
        }

        @media (max-width: 477px) {
            width: 80%;
        }

        @media (max-width: 385px) {
            width: 90%;
        }

        @media (max-width: 350px) {
            width: 100%;
        }

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