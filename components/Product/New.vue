<script setup lang="ts">
import {
  AlertDialog,
  AlertDialogAction,
  AlertDialogCancel,
  AlertDialogContent,
  AlertDialogDescription,
  AlertDialogFooter,
  AlertDialogHeader,
  AlertDialogTitle,
  AlertDialogTrigger,
} from '@/components/ui/alert-dialog';
import { Input } from '@/components/ui/input'


const { loading, open } = useHelpers();

const createNewProduct = async () => {
    try {
        loading.value = true;
    } catch (err) {

    } finally {
        loading.value = false;
        open.value = false;
    }
}

</script>

<template>
  <AlertDialog :open="open">
    <AlertDialogTrigger>
        <Button @click="open = true">Add a new product</Button>
    </AlertDialogTrigger>
    <AlertDialogContent>
      <AlertDialogHeader>
        <AlertDialogHeader>Create a new product</AlertDialogHeader>
        <Input placeholder="My product name"/>
      </AlertDialogHeader>
      <AlertDialogFooter>
        <AlertDialogCancel @click="open = false">Cancel</AlertDialogCancel>
        <AlertDialogAction @click="createNewProduct">Create</AlertDialogAction>
      </AlertDialogFooter>
    </AlertDialogContent>
  </AlertDialog>
</template>