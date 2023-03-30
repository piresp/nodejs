

const mongoose = require('mongoose');

const CustomerSchema = new mongoose.Schema({
  email: { type: String, required: true },
  password: { type: String, required: true },
  trust: { type: Number, required: true },
  cart: {
    products: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Product' }],
  },
  token: { type: String, required: true },
});

const ManagerSchema = new mongoose.Schema({
  email: { type: String, required: true },
  password: { type: String, required: true },
  companies: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Company' }],
  token: { type: String, required: true },
});

const CompanySchema = new mongoose.Schema({
  name: { type: String, required: true },
  cnpj: { type: String, required: true },
  products: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Product' }],
  employees: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Customer' }],
});

const ProductSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String, required: true },
  image: { type: String, required: true },
  last_update: { type: Date, default: Date.now() },
  data_current: {
    customers: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Customer' }],
    price: { type: Number, required: true },
    votes: { type: Number, required: true },
  },
  data_possible: {
    customers: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Customer' }],
    price: { type: Number },
    votes: { type: Number },
  },
  company: { type: mongoose.Schema.Types.ObjectId, ref: 'Company' },
});

const Customer = mongoose.model('Customer', CustomerSchema);
const Manager = mongoose.model('Manager', ManagerSchema);
const Company = mongoose.model('Company', CompanySchema);
const Product = mongoose.model('Product', ProductSchema);

module.exports = {
  Customer,
  Manager,
  Company,
  Product,
};




schema Compare

Customer: {
	_id: string,
	email: string,
	password: string,
	trust: number,
	cart: {
		products: Product[],
	},

	token: string,
};

Manager: {
	_id: string,
	email: string,
	password: string,
	companies: Company[],
	token: string,
}

Company: {
	_id: string,
	name: string,
	cnpj: string,
	products: Product[],
	employees: Customer[],
};

Product: {
	_id: string,
	title: string,
	description: string,
	image: ...,
	last_update: string,
	
	data_current: {
		customers: Customer[],
		price: number,
		votes: number
	},

	data_possible?: {
		customers: Customer[],
		price: number,
		votes: number
	},

	company: Company,
};


