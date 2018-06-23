# README

Try active_storage

Things you may want to cover:

* Ruby version
  * 2.5.1

* System dependencies
  * rails active_storage:install
  * rails db:migrate

* Configuration
  * config/storage.yml
  * environments/xxx.rb


* Ref
  * https://medium.com/@ebifurai_tsn/active-storage-after-rails-5-2-26ad89c93b57
  * Model

    ```bash
    $ rails g scaffold User name
    $ rails db:migrate
    # app/models/user.rb
    class User < ApplicationRecord
      has_one_attached :avatar
      has_many_attached :documents
    end
    $ rails c
    > User.create(name: 'test')
    # will get 2 more methods by default
    > User.first.avatar
    > User.first.documents
    ```

  * View

    ```bash
    # app/views/users/_form.html.erb
    <div class="field">
        <%= form.label :avatar %>
        <%= form.file_field :avatar %>
    </div>
    <div class="field">
        <%= form.label :documents %>
        <%= form.file_field :documents, multiple: true %>
    </div>
    # app/views/users/show.html.erb
    <% if @user.avatar.attached? %>
      <%= image_tag(@user.avatar) %>
    <% end %>
    </p>
    <% if @user.documents.attached? %>
      <p> 
      <h2>Download Documents</h2>
      <% @user.documents.each_with_index do |doc, i| %>
        <p> 
        <%= link_to("doc##{i}", rails_blob_path(doc, disposition: "attachment")) %>
        </p>
      <% end %>
      </p>
    <% end %>
    ```

  * Controller

    ```bash
    # Never trust parameters from the scary internet, only allow the white list through.
    def user_params
      params.require(:user).permit(:name, :avatar, documents: []) 
    end
    ```

  * Try now

    ```bash
    rails s
    ```
