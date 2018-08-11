# Laravel-Notes

1) Creating a Model:
php artisan make:model Models\Balance -m or --migration (creates a model Balance in the Folder App\Models\ and a migration as well)
the migration file will be under the folder database\migrations with a generic table structure
public function up()
    {
        Schema::create('payments', function (Blueprint $table) {
            $table->increments('id');
            $table->timestamps();
        });
    }
	
2) Create a Factory: (https://github.com/fzaninotto/Faker)
$factory->define(App\Models\Balance::class, function (Faker $faker)
{
    return [
        'balance_user_id'     => User::inRandomOrder()->first()->id,
        'balance_paid_todate' => ($faker->numberBetween($min = 1, $max = 10))*112000,
        'balance_due_todate'  => ($faker->numberBetween($min = 1, $max = 10))*57000,
    ];
});

3) php artisan make:seed SeedBalanceTable creates a seed to be injected

class SeedBalanceTable extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        DB::statement('SET FOREIGN_KEY_CHECKS=0');
        Balance::truncate();
        factory(App\Models\Balance::class, 100)->create();
    }
}

4) Seed the table: php artisan db:seed --class SeedBalanceTable

