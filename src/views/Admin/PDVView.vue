<script setup>
import { ref } from 'vue';

const events = ref([
    {
        status: 'Reserva Solicitada',
        date: '15/10/2023 10:30',
        icon: 'pi pi-calendar-plus',
        color: '#9C27B0',
        image: 'reserva-solicitada.jpg',
        sender: 'João Silva',
        receiver: 'Maria Oliveira'
    },
    {
        status: 'Reserva Confirmada',
        date: '15/10/2023 14:00',
        icon: 'pi pi-check',
        color: '#673AB7',
        sender: 'Maria Oliveira',
        receiver: 'Carlos Souza'
    },
    {
        status: 'Em Uso',
        date: '15/10/2023 16:15',
        icon: 'pi pi-play',
        color: '#FF9800',
        sender: 'Carlos Souza',
        receiver: 'Ana Lima'
    },
    {
        status: 'Reserva Concluída',
        date: '16/10/2023 10:00',
        icon: 'pi pi-calendar-check',
        color: '#607D8B',
        sender: 'Ana Lima',
        receiver: 'João Silva'
    }
]);

const reservationInfo = ref({
    reservationId: '12345',
    dataReserva: '15/10/2023 10:30',
    cliente: 'João Silva',
    tipoCampo: 'Futebol',
    status: 'Solicitada',
    urgencia: 'Alta',
    origem: 'Website',
    impacto: 'Alto',
    prioridade: 'Alta',
    localizacao: 'São Paulo',
    aprovacao: 'Aprovado',
    requerente: 'João Silva',
    observador: 'Maria Oliveira',
    atribuidoPara: 'Carlos Souza'
});

const response = ref('');
const additionalInfo = ref('');
const newUrgency = ref(reservationInfo.value.urgencia);
const acceptReservation = ref(false);
</script>

<template>
    <div class="container mx-auto p-4">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
            <div class="card p-4">
                <div class="font-semibold text-xl mb-4">Informações da Reserva</div>
                <p><strong>ID da Reserva:</strong> {{ reservationInfo.reservationId }}</p>
                <p><strong>Data da Reserva:</strong> {{ reservationInfo.dataReserva }}</p>
                <p><strong>Cliente:</strong> {{ reservationInfo.cliente }}</p>
                <p><strong>Tipo de Campo:</strong> {{ reservationInfo.tipoCampo }}</p>
                <p><strong>Status:</strong> {{ reservationInfo.status }}</p>
                <p><strong>Urgência:</strong> {{ reservationInfo.urgencia }}</p>
                <p><strong>Origem:</strong> {{ reservationInfo.origem }}</p>
                <p><strong>Impacto:</strong> {{ reservationInfo.impacto }}</p>
                <p><strong>Prioridade:</strong> {{ reservationInfo.prioridade }}</p>
                <p><strong>Localização:</strong> {{ reservationInfo.localizacao }}</p>
                <p><strong>Aprovação:</strong> {{ reservationInfo.aprovacao }}</p>
                <p><strong>Requerente:</strong> {{ reservationInfo.requerente }}</p>
                <p><strong>Observador:</strong> {{ reservationInfo.observador }}</p>
                <p><strong>Atribuído para:</strong> {{ reservationInfo.atribuidoPara }}</p>
            </div>
            <div class="card p-4">
                <div class="font-semibold text-xl mb-4">Responder Reserva</div>
                <div class="flex flex-col gap-4">
                    <Textarea v-model="response" placeholder="Digite sua resposta" rows="5" cols="30" />
                    <InputText v-model="additionalInfo" placeholder="Informações adicionais" />
                    <div class="flex items-center gap-2">
                        <label for="acceptReservation" class="mr-2">Aceitar Reserva:</label>
                        <Checkbox id="acceptReservation" v-model="acceptReservation" />
                    </div>
                    <div class="flex items-center gap-2">
                        <label for="newUrgency" class="mr-2">Modificar Urgência:</label>
                        <Dropdown id="newUrgency" v-model="newUrgency" :options="['Baixa', 'Média', 'Alta']" placeholder="Selecione a urgência" />
                    </div>
                    <Button label="Enviar Resposta" class="mt-2" />
                </div>
            </div>
        </div>
        <div class="card p-4">
            <div class="font-semibold text-xl mb-4">Reservas</div>
            <Timeline :value="events" align="alternate" class="customized-timeline">
                <template #marker="slotProps">
                    <span class="flex w-8 h-8 items-center justify-center text-white rounded-full z-10 shadow-sm" :style="{ backgroundColor: slotProps.item.color }">
                        <i :class="slotProps.item.icon"></i>
                    </span>
                </template>
                <template #content="slotProps">
                    <Card class="mt-4">
                        <template #title>
                            {{ slotProps.item.status }}
                        </template>
                        <template #subtitle>
                            {{ slotProps.item.date }}
                        </template>
                        <template #content>
                            <img v-if="slotProps.item.image" :src="`https://primefaces.org/cdn/primevue/images/product/${slotProps.item.image}`" :alt="slotProps.item.status" width="200" class="shadow-sm" />
                            <p>
                                <strong>Enviado por:</strong> {{ slotProps.item.sender }}<br />
                                <strong>Recebido por:</strong> {{ slotProps.item.receiver }}
                            </p>
                            <p>
                                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Inventore sed consequuntur error repudiandae numquam deserunt quisquam repellat libero asperiores earum nam nobis, culpa ratione quam perferendis esse,
                                cupiditate neque quas!
                            </p>
                            <Button label="Leia mais" text></Button>
                        </template>
                    </Card>
                </template>
            </Timeline>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@media screen and (max-width: 960px) {
    ::v-deep(.customized-timeline) {
        .p-timeline-event:nth-child(even) {
            flex-direction: row !important;

            .p-timeline-event-content {
                text-align: left !important;
            }
        }

        .p-timeline-event-opposite {
            flex: 0;
        }

        .p-card {
            margin-top: 1rem;
        }
    }
}
</style>
