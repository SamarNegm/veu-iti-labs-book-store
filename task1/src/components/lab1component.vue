<template>
 <!-- task1 -->

 <!-- <ul>
            <li v-for="book in books" :title="book.author">{{book.name}}</li>
 </ul> -->

 <!-- task2 -->
         <div class="row bg-dark justify-content-between p-2">
            <div class="d-flex justify-content-between align-items-baseline">
                <a href="#" class="btn" style="color:yellow;text-decoration:none;" @click.prevent="getBooks"> Books</a>
                <div style="color:white">
                    <span class="p-2" style='color:yellow'>{{list.length}} </span><span v-if="list.length !=1">
                        books</span><span v-if="list.length ==1">book</span><span class="me-2"> In The List</span>
                    <button class=" btn btn-primary p-2 m-2" @click="changeView">list</button>
                </div>
            </div>
        </div>

        <div v-show="!visableWathchList" class="row justify-content-between mt-2">
            <div v-for="book in books" class="card text-center m-2" style="width:18rem">
                <img :src="book.image"
                    style="width: 250px; height: 300px; margin-left:auto;margin-right: auto; margin-top: 10px;">
                <h3 style=" color: rgb(63, 151, 185); padding: 10px;">{{book.name}}</h3>
                <div class="d-flex justify-content-between m-2">
                    <span>{{book.category}}</span>
                    <span>{{book.author}}</span>
                </div>
                <div class="d-flex justify-content-between m-2">
                    <span :class='book.pages>=50 ?"more": "less"'>{{book.pages}}</span>
                    <span>{{currencyFormatter(book.price)}}</span>
                </div>
                <div class="d-flex justify-content-between align-items-baseline m-2">
                    <span>{{book.ISBN}}</span>
                    <button class="btn btn-primary p-2 m-3" v-if="!checkexistence(book)" @click="addBook(book)"
                        style="background-color: rgb(63, 151, 185);">Add to
                        list</button>
                    <span v-if="checkexistence(book)"
                        style="background-color: rgb(194, 216, 241); padding: 10px; border-radius: 7px;"> this Book
                        already in your list</span>
                </div>
            </div>
        </div>
        <div v-show="visableWathchList" class="row">
            <p v-if="list.length == 0" class="text-center fs-4 alert-danger">You don' t have any books in your
                list</p>
            <table v-if="list.length >= 1" class="table">
                <thead>
                    <th>ISBN</th>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Author</th>
                    <th>Pages</th>
                    <th>Remove</th>
                    <th>Price</th>
                </thead>
                <tbody>
                    <tr v-for="wished in list">
                        <td>{{wished.ISBN}}</td>
                        <td>{{wished.name}}</td>
                        <td>{{wished.category}}</td>
                        <td>{{wished.author}}</td>
                        <td :class='wished.pages>=50 ?"more": "less"'>{{wished.pages}}</td>
                        <td><button class="btn btn-danger" @click="removebook(wished)">Remove</button></td>
                        <td>{{currencyFormatter(wished.price)}}</td>
                    </tr>
                </tbody>
                <tfoot>
                    <tr>
                        <th colspan="3" class="text-center fw-bolder"> Total Price:</th>
                        <th colspan="4" class="text-center fw-bolder">{{currencyFormatter(getTotalPrice())}}</th>
                    </tr>
                    <tr>
                        <th colspan="3" class="text-center fw-bolder">Taxes:</th>
                        <th colspan="7" class="text-center fw-bolder">{{currencyFormatter(getTotalPrice()* 0.1) }}</th>
                    </tr>
                    <tr>
                        <th colspan="3" class="text-center fw-bolder">Grand Total:</th>
                        <th colspan="7" class="text-center fw-bolder">{{currencyFormatter(getTotalPrice()* 0.1 +
                            getTotalPrice())}}</th>
                    </tr>
                </tfoot>
            </table>
        </div>
</template>

<script>
import bookss from './Books'
export default {
     data: () => ({
                list: [

                ],
                books: bookss,
                visableWathchList: false
            }),
            methods: {
                changeView() {
                    this.visableWathchList = !this.visableWathchList;
                },
                addBook(book) {
                    this.list.push(book)
                },

                checkexistence(book) {
                    for (let i = 0; i < this.list.length; i++) {
                        if (book.ISBN == this.list[i].ISBN) {
                            return true;
                        }
                    }
                    return false
                },
                getBooks() {
                    this.visableWathchList = false;
                },
                removebook(book) {
                    let boook;
                    for (let i = 0; i < this.list.length; i++) {
                        if (book.ISBN == this.list[i].ISBN) {
                            boook = i;
                        }
                    }
                    this.list.splice(boook, 1);
                },
                getTotalPrice() {
                    let total = 0;
                    for (let i = 0; i < this.list.length; i++) {
                        total += this.list[i].price;
                    }
                    return total;
                },
                currencyFormatter(value) {
                    let formatter = Intl.NumberFormat("ar-SA", {
                        style: "currency",
                        currency: "SAR",
                        minimumFractionDigits: 0
                    })
                    return formatter.format(value)
                }
            }
}
</script>