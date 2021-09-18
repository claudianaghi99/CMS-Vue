<template>
    <Employee></Employee>
    <Modal></Modal>
</template>

<script>
import Employee from "../components/Employee.vue"
import Modal from "../components/Modal.vue"

export default{
    name:"App",
    components:{
        Employee,
        Modal,
    },
};
</script>